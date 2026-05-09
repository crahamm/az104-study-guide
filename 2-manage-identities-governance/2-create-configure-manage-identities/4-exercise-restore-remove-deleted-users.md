Exercise - restore or remove deleted users
==========================================

**Exercise environment needs** \- this lab assumes you have a basic Microsoft Entra tenant with at least User Administrator rights to complete it. You can get a free trial subscription at [Try Microsoft Azure for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn_4b2d05e1-1f36-153c-37cf-c61a47f70fe5).

Remove a user from Microsoft Entra ID
-------------------------------------

1.  Browse to the [Microsoft Entra admin center](https://entra.microsoft.com/).

2.  In the left navigation, under **Identity**, select **Users**.

3.  In the **Users** list, select the check box for a user to delete. For example, select **Chris Green**.

     Tip

    Selecting users from the list allows you to manage multiple users at the same time. If you select the user, to open that user's page, you'll only be managing that individual user.

    ![Screenshot of Microsoft Entra ID all users' list with one user check box selected.](https://learn.microsoft.com/en-us/training/wwl-sci/create-configure-manage-identities/media/remove-user.png)

4.  With the user account selected, on the menu, select **Delete user**.

5.  Review the dialog box and then select **OK**.

Restore a deleted user
----------------------

You can see all the users that were deleted less than 30 days ago. These users can be restored.

1.  In the Users page, in the left navigation, select **Deleted users**.

2.  Review the list of deleted users and select the user you deleted.

    **Important:** By default, deleted user accounts are permanently removed from Microsoft Entra ID automatically after 30 days.

3.  On the menu, select **Restore user**.

4.  Review the dialog box and then select **OK**.

5.  In the left navigation, select **All users**.

6.  Verify the user was restored.
