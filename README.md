# Wso2

# Enabling Email notifications in WSO2 API Manager with your Gmail account

In WSO2 API Manager you can enable notifications at the creation of new API versions in order to notify existing subscribers (via email) that a new version of the API is available. Once this is configured existing subscribed will be getting emails when a new version of the API is released.
First we need to have a subscriber account to log into WSO2 API Store. Log in to the Management Console, make sure the subscribed user has email address in user profile. For this example I have updated admin user with my email address


Verify subscribed user has email address
2. In the Management Console click Main > Resource > Browse. Search for /_system/config/apimgt/applicationdata/tenant-conf.json file and click Edit as Text. Set the NotificationsEnabled property to true.

“NotificationsEnabled”:”true”,
“Notifications”:[{
“Type”:”new_api_version”,

# 3. Now we need to configure API Manager server to send emails for a new version notification. For this, go to <APIM_HOME>/repository/conf/output-event-adapters.xml file under the <adapterConfig type=”email”> section. Provide a valid email address which can be used to send these emails. I have chosen a gmail address hence the email would be in the form of xxxx@gmail.com

<adapterConfig type=”email”>
<! — Comment mail.smtp.user and mail.smtp.password properties to support connecting SMTP servers which use trust
based authentication rather username/password authentication →
<property key=”mail.smtp.from”>xxxxxx@gmail.com</property>
<property key=”mail.smtp.user”>xxxxxx@gmail.com</property>
<property key=”mail.smtp.password”>[add password]</property>
<property key=”mail.smtp.host”>smtp.gmail.com</property>
<property key=”mail.smtp.port”>587</property>
<property key=”mail.smtp.starttls.enable”>true</property>
<property key=”mail.smtp.auth”>true</property>
<! — Thread Pool Related Properties →
<property key=”minThread”>8</property>
<property key=”maxThread”>100</property>
<property key=”keepAliveTimeInMillis”>20000</property>
<property key=”jobQueueSize”>10000</property>
</adapterConfig>
  
# 4. When you are using a Google mail account, Google has restricted third-party apps and less secure apps from sending emails by default. Therefore, we need to configure your account to disable this restriction.
Go to https://myaccount.google.com/security
In ‘Signing in to Google’ section make sure that the 2-step Verification is disabled or off.
In ‘Less secure app access’ section and enable Allow less secure apps.


Enable less secure app access
# 5. The configurations are complete now. Go to API store and create a new version of the API and publish it. All the subscribed users with valid email address will get notifications now as follows.


Email notification from WSO2 API Manager


Email body
References
[1] https://docs.wso2.com/display/AM260/Enabling+Notifications

[2] https://docs.wso2.com/display/AM260/Configuring+Alerts#ConfiguringAlerts-Editalertsasbusinessrules
