Exercise - Grant access using Azure RBAC and the Azure portal
=============================================================

A coworker named Alain at First Up Consultants needs permission to create and manage virtual machines for a project on which they're working. Your manager has asked that you handle this request. Using the best practice to grant users the least privileges to get their work done, you decide to assign Alain the Virtual Machine Contributor role for a resource group.

Grant access
------------

Follow this procedure to assign the Virtual Machine Contributor role to a user at the resource group scope.

1.  Sign in to the [Azure portal](https://portal.azure.com/) as an administrator that has permissions to assign roles, such as [User Access Administrator](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) or [Owner](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#owner).

2.  In the Search box at the top, search for **Resource groups**.

    ![Screenshot of the Azure portal that shows how to search for resource groups.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-resource-groups.png)

3.  In the list of resource groups, select a resource group.

    These steps use a resource group named **example-group**, but your resource group's name will be different.

4.  On the left menu pane, select **Access control (IAM)**.

5.  Select the **Role assignments** tab to display the current list of role assignments at this scope.

    ![Screenshot showing Role assignments tab for the selected resource group.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-resource-group-role-assignment.png)

6.  Select **Add** \> **Add role assignment**.

    If you don't have permissions to assign roles, the **Add role assignment** option will be disabled.

    ![Screenshot that shows Add role assignment menu.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-resource-group-add-role-assignment.png)

    The **Add role assignment** page opens.

7.  On the **Role** tab, search for and select **Virtual Machine Contributor**.

    ![Screenshot that shows Add role assignment and list of roles.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-select-role.png)

8.  Select **Next**.

9.  On the **Members** tab, select **Select members**.

10.  Search for and select a user.

    ![Screenshot of the add role assignment page that shows the select members option.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-select-members-option.png)

11.  Select **Select** to add the user to the Members list.

12.  Select **Next**.

13.  On the **Review + assign** tab, review the role assignment settings.

14.  Select **Review + assign** to assign the role.

    After a few moments, the user is assigned the Virtual Machine Contributor role at the resource group scope. The user can now create and manage virtual machines just within this resource group.

    ![Screenshot that shows the Virtual Machine Contributor role assigned to a user.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-vm-contributor-assignment.png)

Remove access
-------------

In Azure RBAC, you can remove a role assignment to remove access.

1.  In the list of role assignments, select **View Assignments**.

2.  Search for and check the box for the user with the Virtual Machine Contributor role.

3.  Select **Delete**.

    ![Screenshot that shows the Remove role assignment message.](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/media/5-remove-role-assignment.png)

4.  In the **Remove role assignments** message that appears, select **Yes**.

In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using the Azure portal.