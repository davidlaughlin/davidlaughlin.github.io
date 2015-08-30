---
layout: post
title: When to catch the Exception class
description: "When is it okay to not follow a best practice."
tags: [exception handling, best practices, c#, .net]
image:
  background: triangular.png
---

Recently, on a popular C# discussion forum, I was involved in a conversation about catching the generic Exception class.  A user had posted a brief code snippet he had discovered why working on a legacy application that looked something similar to:

{% highlight c# %}

public static class LoggerUtil
{
  // ... snip

  public static void WriteLog(public string message, LogSeverity severity)
  {
    try
    {
      LogEntry entry = new LogEntry();
      entry.Message = message;
      entry.Severity = severity;
      Logger.Write(entry);
    }
    catch (Exception ex)
    {
      LogEntry entry = new LogEntry();
      entry.Message = "Log Failure!";
      entry.Severity = LogSeverity.Error;
      Logger.Write(entry, ex);
    }
  }

  // ... snip
}

{% endhighlight %}
