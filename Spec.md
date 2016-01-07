Sprocket
========

Abstract
--------

Sprocket's design revolves around the use of **streams**. These consolidate
various things like autonomous sequencing and joystick inputs into a single
sequence of actions to take.

Internally, streams are represented by queues, a FIFO (first-in first-out) data structure, where the first (oldest) entry is read out first.

## Streams

There are two main stream categories:
- **Input** (joystick input)
- **Subsystem** (robot components, one stream each)

## Functions

The functions operating on the streams are as follows:
1. Write - pipe actions into **Input** stream
2. Delegate - separate **Input** stream by subsystem
3. Prioritize - reject actions with lower priority, rush actions with higher priority, pipe into **Subsystems**
4. Read - pipe actions out of **Subsystem** streams

**Write** and **Read** correspond to the queue "Enqueue" and "Dequeue" VIs.

## Data Types

The data type of the streams has three parts that can be configured by the user.
- Name - enum describing the action
- Priority - a signed 32-bit (word) integer
- Data - a variant data, for user-defined data types

This library uses variants. Users are given the responsibility to convert to and from variants properly.

For more information, please visit the [NI documentation](http://www.ni.com/white-paper/4998/en/).

## Priority
Priority is designed with two principles:
- Higher priorities **interrupt**.
- Lower priorities are **ignored**.

What this means in practice is simple:
- If a higher-priority action is piped into a stream with a lower-priority action waiting, the stream is cleared, making the action the next task.
- If a lower-priority action is piped into a stream with a higher-priority action waiting, it is not added to the stream.

This means that only actions of equal priority may be chained.

## Design Decisions

### Priority

Priority was made a signed integer, and not unsigned. While the idiomatic style is to make 0 the lowest priority, if users ever need to make something of lower priority they can.
