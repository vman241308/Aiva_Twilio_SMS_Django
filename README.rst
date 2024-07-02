Aiva-VoiceBot-Twilio
=================

Quickstart
----------

1. Include ``Aiva_Twilio_SMS_Django`` in your ``requirements.txt`` file.

2. Add ``Aiva_Twilio_SMS_Django`` to ``INSTALLED_APPS`` and syncdb/migrate.

3. Add the following url to your urlconf:
   
   .. code-block:: python

       url(r"^messaging/", include("Aiva_Twilio_SMS_Django.urls")),

   this will receive confirmation callbacks for any SMS message
   that you send using ``utils.send_sms``.

4. Create a new view and override ``IncomingSMSView.post_save(self, obj)`` method
   to receive SMS messages via callbacks from Twilio. The received ``obj``
   param will be an instance of ``IncomingSMS`` model.

5. Configure Twilio callback to send notifications to the above view's url.

6. Configure settings:

   - TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN, TWILIO_PHONE_NUMBER - copy
     credentials from the Twilio panel.

   - TWILIO_CALLBACK_USE_HTTPS - use https or not for delivery confirmation
     callback urls.
   
   - TWILIO_CALLBACK_DOMAIN - optionally set domain name or IP of your site
     (otherwise the server name will be extracted from the request info).
   
   - TWILIO_DRY_MODE - set if you want to run in test mode.
