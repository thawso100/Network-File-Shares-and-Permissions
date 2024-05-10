<p align="center">
<img src="https://i.imgur.com/MTZBOBN.png" alt="Azure Logo"/>
</p>
<h1>Network File Shares and Permissions</h1>

<h2>Create some sample file shares with various permissions</h2>

- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as a normal user (mydomain\<someuser>)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
- Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
- Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
- Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
- (Skip accounting for now)

<p> we first needed to create two vireture machine (VM) DC-1 and Client-1 in Azure</p>
<img src="https://i.imgur.com/ZIIzueu.png" height="80%" width="80%" alt="image"/>
<p> As we log in to the DC-1 we will create four folder 
- read access 
- write access 
- no access 
- accounting 
- Set the following permissions (share the folder) for the “Domain Users” group:
</p>
<img src="https://i.imgur.com/devr9Wx.png" height="80%" width="80%" alt="image"/>
<img src="https://i.imgur.com/KwVXrfq.png" height="80%" width="80%" alt="image"/>
<P> For the write-access we will give a permission to "read/write" </P>
<img src="https://i.imgur.com/Xb4tfas.png" height="80%" width="80%" alt="image"/>

<h2>Attempt to access file shares as a normal user</h2>

- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?


<P> Let's us to go Client-1 and go to \\dc-1 , we will see the file and let's interact with the write access file </P>
<img src="https://i.imgur.com/ziqElIJ.png" height="80%" width="80%" alt="image"/>
<img src="https://i.imgur.com/60hNtDF.png" height="80%" width="80%" alt="image"/>

<P> As you can see, we can created a text document with "hello!!" in there the foler  </P>
<img src="https://i.imgur.com/JWqhKF3.png" height="80%" width="80%" alt="image"/>

<P>we can also go back to DC-1 to see if the the text appearing </P>
<img src="https://i.imgur.com/NFN9c4C.png" height="80%" width="80%" alt="image"/>
<img src="https://i.imgur.com/XPT4ShM.png" height="80%" width="80%" alt="image"/>


<h2>Create an “ACCOUNTANTS” Security Group, assign permissions, an test access </h2>

- Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
- On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
- On Client-1, as  <jos.sap>, try to access the accountants folder. It should fail. 
- Log out of Client-1 as  <jos.sap>
- On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
- Sign back into Client-1 as <jos.sap> and try to access the “accounting” share in \\DC-1\ - Does it work now?

<P> In DC-1 in Active Directory users and computers and we will a security group and in that we will create a group called " ACCOUNTANTS"  </P>
<img src="https://i.imgur.com/MHH6bDQ.png" height="80%" width="80%" alt="image"/>
<img src="https://i.imgur.com/Ijn3xko.png" height="80%" width="80%" alt="image"/>

<P> we will also allow the "ACCOUNTANTS" group to have access to read and write </P>
<img src="https://i.imgur.com/UD7t6Uv.png" height="80%" width="80%" alt="image"/>

<P> Once we the "ACCOUNTATNS" permission to read and write let's go to Client-1 and see we have access to it or not. We cannot access the file because the "Client-1 user "jos.sap" is not listed as a member of the accountatns </P>
<img src="https://i.imgur.com/0cmfc3S.png" height="80%" width="80%" alt="image"/>
<img src="https://i.imgur.com/9YmUaMP.png" height="80%" width="80%" alt="image"/>

<P> Now let's go to DC-1 and add user " jos.sap" as a member of the accountants </P>
<img src="https://i.imgur.com/CzuczxF.png" height="80%" width="80%" alt="image"/>

<P> for the last and final time, we need to logoff from " client -1" and login back again with the user of " jos.sap" and this time we have the access to the accountants file </P>
<img src="https://i.imgur.com/cYJColW.png" height="80%" width="80%" alt="image"/>





