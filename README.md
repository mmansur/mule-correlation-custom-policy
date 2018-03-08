# mule-correlation-custom-policy
API Manager custom policy to generate correlation id

Splunk Query:

host="127.0.0.1" | spath application | spath muleMessageId | spath notificationType | spath customEventProperties.alc-correlation | transaction muleEventId, customEventProperties.alc-correlation | search customEventProperties.alc-correlation="ALC-ID-92a3fde7-609a-4a21-b745-732bf7305d1e" | eval exception_occured=if(action="exception",200,10) | eval previous_application = case (application = "Product-sAPI", "Omni-Channel-xAPI", application = "Customer-sAPI", "Omni-Channel-xAPI", application = "Order-sAPI", "Order-Fulfillment-pAPI", application = "Notifications-sAPI", "Order-Fulfillment-pAPI", application = "Order-Fulfillment-pAPI", "Omni-Channel-xAPI") | table previous_application, application, exception_occured | dedup previous_application, application
