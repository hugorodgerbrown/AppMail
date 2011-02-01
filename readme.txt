AppMail is (will be) an application for sending emails for use within larger applications.

1. Templates / templating - UI to upload HTML / plain text email templates
2. API to allow for per-email sending - upload JSON payload, email info (to/from/subject etc.)
3. API to provide stats on emails sent, record times/dates, allow for searching by recipient / template etc.
4. API to support bulk uploads (multiple emails)
5. Preview function
6. Callback function / Web hook for failed emails 
7. Ability to use different email services for the actual sending - native AppEngine mail, Amazon SES, corporate SMTP

Why bother?

Complex transactional sites (think ecommerce) can have 10s of system-generated notification emails - account created, order confirmed, password lost, etc. Whilst most web frameworks have mail apis for the sending of messages, there is often a lot of work required to plug the core "send email" function into an application - defining templates, dynamic data etc., combined with the sort of system monitoring that a large implementation requires. If you want to know how many emails you are sending, to confirm whether a specific email was sent ("I never received my order confirmation email", etc.) there can be a lot of work involved in implementation. AppMail is designed to provide DEVELOPERS with a simple api that they can use to manage this. It is NOT intended (at first) for marketing teams or content managers to use - this is a tool to make developers' lives easier. 

There are lots of commercial email services available, but where they provide an API they typically require the user to post the entire HTML contents of the mail to the API - the key to AppMail is having the templates uploaded to the system, and then simply posting the payload (e.g. order details) to the appropriate template.

The initial implementation will be deployed to AppEngine (free, easy to use).

1. Create the HTML template
2. Upload the template to AppMail, giving it a unique name (e.g. "OrderConfirmation")
3. Add in a call to the SendMail api in the appropriate location

{
  SendMail: {
    To: "recipient",
    From: "Sender",
    Subject: "Subject",
    Template: "OrderConfirmation",
    WebHook: "http://myapp.appspot.com/appmail/callback",
    Payload: {
      FirstName: "Hugo",
      LastName: "Rodger-Brown",
      OrderDetails: {
        TrackingNumber: "123456"
      }
    }
  }
}