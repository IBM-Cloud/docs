

# SendGrid troubleshooting
{: #ts_sendgrid}

Here is the answer to a question about using SendGrid in {{site.data.keyword.Bluemix}}.



## Unable to send emails by using SendGrid
{: #ts_sendgrid_email}

If you are unable to send emails by using the SendGrid service, you might have reached the limit of emails that are allowed per service instance.

**What's happening**

After you have sent the maximum number of emails that are allowed, you are unable to use the SendGrid service to send more emails.

**Why it's happening**

When you send emails by using the SendGrid service, you are limited to sending 25,000 emails per service instance each month. After you have reached the limit, SendGrid stops sending emails, and further charges are not incurred for using this service.

To check the remaining number of emails that are allowed, click your SendGrid service instance from the {{site.data.keyword.Bluemix_notm}} dashboard, and then click **OPEN SENDGRID DASHBOARD**. You can see the number in the **Credits Remaining** field.


**How to fix it**

If you want to send more emails after you reached the limit of 25,000 emails per service instance each month, you can add another service instance. For more information about SendGrid, see Getting Started with SendGrid.
