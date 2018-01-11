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
