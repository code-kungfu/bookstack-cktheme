## Code-Kungfu Theme for BookStack

A theme for the [BookStack](https://www.bookstackapp.com) Wiki software.

---

### Preface
Out of the box, BookStack does not allow you to toggle the display of **Recent Activity**, who has created / updated an element, shown in **Details** box and **Revisions Browser**. For privacy reasons, more often than not, you want to limit who can view recent activity and who has created or updated an element in BookStack.

Thanks to the well thought out structure of BookStack and good software design by the author of BookStack, [Dan Brown](https://github.com/ssddanbrown), the Visual Theme System allows us to do customization without changes to the core. This also allows the changes to survive an upgrade of BookStack!.

Please go support Dan and his BookStack project, in any way possible. This is an amazing piece of software.

---

### Installation

The theme uses the Visual Theme System exposed in BookStack to perform the least invasive changes.

Warning: Make sure to make a backup of your database before proceeding.

To achieve the granular access control on a per-role basis, we need to manually add two new **role_permissions** to the database.
The two new role permissions are:

- **view-recent-activity** - This will control whether or not the Recent Activity should be visible in the various areas where it is present.
- **view-extended-activity** - This will control the access to the Revisions sub-page of a given element and also hide who the author has created or updated an element.

These permissions will be available as system permissions you can toggle in the role editor, when editing a role:
- Show recent activity
- Show extended activity


Please note, this is unsupported and could possibly break in a future release of BookStack. - You have been warned! 

1) First, clone this repository to a location of your choice.
2) Copy the whole folder **cktheme** to the themes folder. The themes folder is found in the root of your BookStack installation.
3) Open your **.env** file located in the root of your BookStack installation in a text editor of choice.
4) After your **APP_URL** variable, add the following line: **APP_THEME=cktheme** and save your **.env** file.
5) Log into your **phpmyadmin** instance which has access to your BookStack database.
6) Before proceeding, read the above warning again.
7) In the BookStack database, locate the **role_permissions** table.
8) Make sure the last permission ID is **78** (**receive-notifications**).
If not, adjust the IDs in the following SQL accordingly.
9) Click on the **SQL** tab in **phpmyadmin** and insert the following SQL:
```sql
INSERT INTO `role_permissions` (`id`, `name`, `display_name`, `description`, `created_at`, `updated_at`) VALUES
(79, 'view-recent-activity', 'View Recent Activity', NULL, '2024-05-24 23:36:00', '2024-05-24 23:36:00'),
(80, 'view-extended-activity', 'View Extended Activity', NULL, '2024-05-24 23:36:00', '2024-05-24 23:36:00');
```
10) Hit the **Go** button and if everything went well, the **role_permissions** table should now have two new permissions!
You can verify  this by refreshing the table.
11) Log into your BookStack instace as Admin. Navigate to **Settings -> Roles**
12) By default the new permissions are unchecked for all roles in BookStack.
Select a role, e.g. Admin and check both **Show recent activity** and **Show extended activity** and hit Save Role.
Now all admins will be able to view Recent Activity and have access to the Revisions browser in a page.

---


### Kudos

- Dan Brown and contributors making BookStack such a great software.
- People in the following Github [issue](https://github.com/BookStackApp/BookStack/issues/1291) who also wanted to control the sidebar content. This is what inspired me to implement this theme in the first place.

---

### Version History

v1.0 - Initial release of the theme. Based on files from BookStack **v24.05.1**

---

### Contributions
Issues and pull-requests are welcome.

---

### License

This theme is licensed under the BSD 3-Clause License.
See [LICENSE](LICENSE) for details.