# This is a custom authentication audit logger to log user-agent, referer, host and cookies in the authentication request

You can write similar code to print whatever you want in the authentication request by following this code structure


1. Once you create the osgi bunddle doing a "mvn clean install"
2. But the built bundle to the <carbon-home>/repository/components/dropins/ folder.
3. Dissable the current AuthenticationAuditor class in <carbon-home>/repository/conf/identity/identity.xml file  under EventListeners

        <EventListener type="org.wso2.carbon.identity.core.handler.AbstractIdentityMessageHandler"
                       name="oorg.wso2.carbon.identity.data.publisher.application.authentication.impl.AuthenticationAuditLogger"
                       orderId="11" enable="false"/>
                       
4. Enable the new authenticationAuditor class in <carbon-home>/repository/conf/identity/identity.xml file  under EventListeners

       <EventListener type="org.wso2.carbon.identity.core.handler.AbstractIdentityMessageHandler"
                       name="org.wso2.carbon.custom.audit.logger.extension.impl.CustomAuthenticationAuditLogger"
                       orderId="11" enable="true"/>
                       
5.Restart the server


output will looks like this
----------------------------

[2018-01-11 14:20:42,781]  INFO {AUDIT_LOG}-  Initiator : admin@carbon.super | Action : Login | Target : ApplicationAuthenticationFramework | Data : { "ContextIdentifier" : "c2de352f-e05d-4f35-acba-b768880b6162","AuthenticatedUser" : "admin@carbon.super","AuthenticatedUserTenantDomain" : "carbon.super","ServiceProviderName" : "wso2_sp_dashboard","RequestType" : "samlsso","RelyingParty" : "wso2.my.dashboard","AuthenticatedIdPs" : "eyJ0eXAiOiJKV1QiLCAiYWxnIjoibm9uZSJ9.eyJpc3MiOiJ3c28yIiwiZXhwIjoxNTE1NjYwNjQyNzQzMzAwMCwiaWF0IjoxNTE1NjYwNjQyNzQzLCJpZHBzIjpbeyJpZHAiOiJMT0NBTCIsImF1dGhlbnRpY2F0b3IiOiJCYXNpY0F1dGhlbnRpY2F0b3IifV19.","user-agent" : "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:57.0) Gecko/20100101 Firefox/57.0","referer" : "https://localhost:9443/authenticationendpoint/login.do?SSOAuthSessionID=888A2782EE39228EE534624BE220DE67A4285F2047B23A2D6AE10CDC0E5483EC2F6EFB6A5EAC8A7B533E6BDCC6902E60921DC273B878479CF5AEA9B3880500987D820ACF49E7587239892673C6D3765EB1C0ADBC0DA27896B251FB46DAD1D6B3FE431BF64752EA92654F3AB032702DAA79C3F39AAAED9130047B003EEA0AE9BD&commonAuthCallerPath=%2Fsamlsso&forceAuth=false&passiveAuth=false&tenantDomain=carbon.super&sessionDataKey=c2de352f-e05d-4f35-acba-b768880b6162&relyingParty=wso2.my.dashboard&type=samlsso&sp=wso2_sp_dashboard&isSaaSApp=true&authenticators=BasicAuthenticator:LOCAL","cookie" : "menuPanel=visible; menuPanelType=config; samlssoTokenId=8a4e0687-a5f4-4675-980d-2f2c075d9995; JSESSIONID=255DF08C7DA1AB7BBC7DFB0BD0D8EA06; commonAuthId=62c1a4d9-1a6b-4138-8905-20dc9854ba5e","Host" : "localhost:9443","Client-ip" : "127.0.0.1" } | Result : Success  
