# Asynchronous Procedure Call (APC)

There are two types of procedure calls: **synchronous** and **asynchronous**. The difference between them is fairly simple:

- **Synchronous calls** execute sequentially on a single thread, where each call waits for the previous one to complete before proceeding.
- **Asynchronous calls** allow a program to start a task and continue executing other operations without waiting for the task to finish.

---

## Structure of an APC

An APC is typically represented as an object with a small memory footprint, which is passed to a service responsible for managing wait intervals. The APC is activated when a specific event occurs (e.g., user input).

The lifecycle of an APC consists of two stages:

- **Passive Stage:** The APC waits for input data.
- **Active Stage:** The APC processes the received data.

There’s also a special type of asynchronous procedure known as an **actor**, which is a reusable procedure with separate input and output ports. One port receives input, while the other handles the processed output provided by the user.

---

## In-Depth: Asynchronous Procedure Calls (APCs)

There are two primary types of APCs: **User APCs** and **Kernel APCs**, with the main difference being control over when they are executed.

- **User APCs:** The target thread has control over when the APC is executed. The thread processes scheduled APCs only when it enters an alertable state by executing one of the following functions:

  - `SleepEx`
  - `SignalObjectAndWait`
  - `WaitForSingleObjectEx`
  - `WaitForMultipleObjectsEx`
  - `MsgWaitForMultipleObjectsEx`

Each of these APIs indicates that the calling thread will be idle temporarily, allowing the system to process scheduled work. The `MsgWaitForMultipleObjectsEx` function, in particular, was introduced by Microsoft to help developers use idle time for scheduled work without the need to handle complex threading.

- **Special APCs:** These behave differently, as the target thread has no control over when they run. The only certainty is that they **won’t execute** when:

  - A system call is in progress, or
  - The thread is in a non-alertable wait state.

Otherwise, the system decides when the special APC will execute, regardless of what the thread is doing. Up until Windows 10, special APCs were only available in kernel mode. They were primarily used for IO completion in device drivers, which don’t depend on the thread they interrupt.

In Windows 11 and later, Microsoft introduced the possibility of using special APCs in user mode. Although the exact reasoning isn’t clear, it might be related to **User Mode Device Drivers**, which don’t run in kernel mode but follow similar design principles. For most application-level development, though, special APCs have limited use and can introduce difficult-to-reproduce bugs.

---

## Credits & References

This explanation and research were inspired by the following resources:

- [Wikipedia: Asynchronous Procedure Call](https://en.wikipedia.org/wiki/Asynchronous_procedure_call)
- [Microsoft Docs: Asynchronous Procedure Calls](https://learn.microsoft.com/en-us/windows/win32/sync/asynchronous-procedure-calls)
- [CodeProject: Understanding Windows Asynchronous Procedure Calls](https://www.codeproject.com/Articles/5355373/Understanding-Windows-Asynchronous-Procedure-Calls)
