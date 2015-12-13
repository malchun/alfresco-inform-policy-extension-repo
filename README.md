# alfresco-inform-policy-extension-repo v0.7

An Alfresco 5.0 extension. Informs interested users about document updates. 

## v0.7
### DONE
* Email metadata customising.
* Correct exceptions and checks
* ~~Check templates in init~~ (hard to make, dropped)

Now you can set prefered Subject and From in global properties of extension. Also, extension changed in way to make it safer for errors.

### Installation
For Linux
* Clone repo `git clone https://github.com/malchun/alfresco-inform-policy-extension-repo`
* In repo folder checkout v0.7 branch `git checkout v0.7`
* Set your preferences in ***{repo-directory}/src/main/amp/config/alfresco/module/alfresco-inform-repo/alfresco-global.properties***
* Run `mvn install` (make sure that you have maven and jdk8 installed)
* Copy the .amp file from ***{repo-directory}/target/*** into ***{alfresco-directory}/amps/***
* Run `./{alfresco-directory}/bin/apply_amps.sh`

***Warning!*** Extension would not work without configured OutboundSMTP!

### Development build
You'll need test models with cm:person assocs for developemnt and debug. Sample model and context for it are located under **src/test/resources/alfresco/extension/**.
* Running embedded Tomcat with `./run.sh` activates it automatically.
* If you need a debug amp to run on external Alfresco, build it with `mvn -Pdevelopment clean package`
* On Share side edit **share-config-custom.xml** to include into **<types/>** section something like this:
```xml
         <type name="cm:content">
               <subtype name="myc:assocs" />
         </type>
```
* After that you can "Change type" of any file into custom **myc:assocs** to get cm:person assocs for debug purposes.

### Usage
This extension allows you to inform users about changes in related documents. All preferences could be set in ***alfresco-global.properties***. This version has next preferences:
* Mail preferences
 * ***mail.from*** (String) - notification from address, not working if in your OutboundSMTP configuration mail.from.enabled false or not set! 
 * ***mail.subject*** (String) - notification subject
* Group preferences
 * ***creator*** (booolean) - enable notifications for document creator
 * ***lasteditor*** (booolean) - same for last editor of document
 * ***associated*** (booolean) - same for everyone in target associations of document
 * ***editors*** (booolean) - and for version creators

Once again: ***you should set them before compiling .amp file!***
After starting Alfresco with installed extension you can find email templates at ***dictionary/Email Templates/Document Change Notification/*** in repository and customize them if you need.
