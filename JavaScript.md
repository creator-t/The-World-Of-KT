# Get about date 

        ```
        let d = new Date();
        let year = d.getFullYear();
        // let month = d.getMonth();
        let day = d.getDay();
        let month = d.getUTCMonth() + 1;
        let UTCDate = d.getDate();
        ```

# How could we call APEX in LWC

        in APEX Class 

        ```
        /**
        * @description
        */
        public with sharing class UseWire {
        /**
        * @description getContacts description
        * @return   return List<Contact> contacts
        */
        @AuraEnabled(cacheable=true)
        public static List<Contact> getContacts() {
                try {
                List<Contact> contacts = [
                        SELECT AccountId, Email, Phone
                        FROM Contact
                ];
                return contacts;
                } catch (Exception e) {
                throw new AuraHandledException(e.getMessage());
                }
        }
        // public useWire() {

        // }
        }
        ```
        In LWC JS

        ```
        import { LightningElement, wire } from "lwc";
        import getContacts from "@salesforce/apex/UseWire.getContacts";
        import refreshApex from "@salesforce/apex";
        export default class sfdxDisplayContacts extends LightningElement {
                contacts;
                error;

                @wire(getContacts)
                wiredContacts({ error, data }) {
                        console.log("this.wiredContacts: ", { error, data });
                        if (data) {
                        this.contacts = data;
                        this.error = undefined;
                        } else if (error) {
                        this.error = error;
                        this.contacts = undefined;
                        }
                }
                refreshContact() {
                        refreshApex(this.wiredContacts);
                }
        }
        ```
# How Could RefreshApex in the before.
# How to solve use github with VS Code problems about :
## unable to access 'https://github.com/creator-t/The-World-Of-tk.git/': SSL certificate problem: self signed certificate in certificate chain

        Open Git Bash and run the command if you want to completely disable SSL verification.

        ```
        git config --global http.sslVerify false
        ```

        Note: This solution opens you to attacks like man-in-the-middle attacks. Therefore turn on verification again as soon as possible:

        ```
        git config --global http.sslVerify true
        ```

        I edited the Git config text file
        C:\Users\ktian019\.gitconfig(PWC's computer)
## fatal: unable to update url base from redirection:asked for: https://github.com/creator-t/The-World-Of-tk.git/info/refs?service=git-upload-pack redirect: http://20.205.243.166:6080/php/urlblock.php?args=AAAAdwAAABD1g1qsIMdXkmuj8XFsDa71AAAAEBuxrr~3vihwHGfXWfc~KucAAABHAAAAR7N0GUoICYSeh7z~iNQoJbFO4wLDqFZWEl5UAdKKCjgFnZ202k38TV67L1ABrcdQD1EK~oGi9ky~unYZEqRMPuiTPXXwqDEw&url=https://github.com%2fcreator-t%2fThe-World-Of-tk.git%2finfo%2frefs%3fservice%3dgit-upload-pack

        ```
        //I connect email and name
        git config --global user.email "you@example.com"
        git config --global user.name "Your Name"
        ```
        ```
        the point is PWC blocks access to github, so log in to GitHub on your browser first, then sync.



