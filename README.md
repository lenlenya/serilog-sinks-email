# Serilog.Sinks.Email

[![Build status](https://ci.appveyor.com/api/projects/status/sfvp7dw8u6aiodj1/branch/master?svg=true)](https://ci.appveyor.com/project/serilog/serilog-sinks-email/branch/master)

Sends log events by SMTP email.

**Package** - [Serilog.Sinks.Email](http://nuget.org/packages/serilog.sinks.email)
| **Platforms** - .NET 4.5

```csharp
var log = new LoggerConfiguration()
    .WriteTo.Email(
        fromEmail: "app@example.com",
        toEmail: "support@example.com",
        mailServer: "smtp.example.com")
    .CreateLogger();
```

An overload accepting `EmailConnectionInfo` can be used to specify advanced options.


重新编译了项目，以处理MailKit版本依赖问题。
在实际开发中，我们引用了一个组件A，它依赖MailKit>=3.4.1,然后就触发了此组件的依赖错误：
> Exception while emitting periodic batch from Serilog.Sinks.PeriodicBatching.PeriodicBatchingSink: System.MissingMethodExce
ption: Method not found: 'System.Threading.Tasks.Task MailKit.MailTransport.SendAsync(MimeKit.MimeMessage, System.Threading.CancellationToken, MailKit.
ITransferProgress)'.
   at Serilog.Sinks.Email.EmailSink.EmitBatchAsync(IEnumerable`1 events)
   at System.Runtime.CompilerServices.AsyncMethodBuilderCore.Start[TStateMachine](TStateMachine& stateMachine)
   at Serilog.Sinks.Email.EmailSink.EmitBatchAsync(IEnumerable`1 events)
   at Serilog.Sinks.PeriodicBatching.PeriodicBatchingSink.OnTick()

