**User Authorization (SUDO)**

On this page, users can be set on which clients to be authorized. To do this, from the menu
Click on create new authorization group button. 'sudoHost', at least one each from 'sudoUser' and 'sudoCommand' properties are added. sudoHost: Indicates which clients will be authorized to operate. The client DN address must be added to this field. Multiple client DN addresses can be added.
sudoCommand: Indicates which commands can be run on clients. (You can add 'ALL' for all commands). More than one command can be added.
sudoUser: Indicates which users will be authorized on the selected clients. User DN address must be added to this field. Multiple user DN addresses can be added

After these operations, authorized users can run the added commands in the sudoCommand field on the added clients.


[![Kullanıcı Yetkilendirme(sudo)](../images/userAuthorizationSudo/userAuthorization.png)](../images/userAuthorizationSudo/userAuthorization.png)
<link href=/lider3.0/assets/style.css rel=stylesheet></link>
