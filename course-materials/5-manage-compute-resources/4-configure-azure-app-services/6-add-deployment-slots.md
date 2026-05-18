Add deployment slots
====================

Deployment slots are configured in the Azure portal. You can swap your app content and configuration elements between deployment slots, including the production slot.

### Things to know about creating deployment slots

Let's review some details about how deployment slots are configured.

-   New deployment slots can be empty or cloned.

-   Deployment slot settings fall into three categories:

        -   Slot-specific app settings and connection strings (if applicable).
        -   Continuous deployment settings (when enabled).
        -   Azure App Service authentication settings (when enabled).
-   When you clone a configuration from another deployment slot, the cloned configuration is editable. Some configuration elements follow the content across the swap. Other slot-specific configuration elements stay in the source slot after the swap.

#### Swapped settings versus slot-specific settings

The following table lists settings that are swapped between deployment slots. The table also lists settings that remain in the source slot (slot-specific). As you review these settings, consider which features are required for your App Service apps. Read more about [which settings are swapped](https://learn.microsoft.com/en-us/azure/app-service/deploy-staging-slots?tabs=portal#which-settings-are-swapped).

| Swapped settings | Slot-specific settings |
| --- |  --- |
| Language stack and version, 32/64-bit App settings **\***Connection strings **\***Mounted storage accounts\* Public certificates WebJobs content Hybrid connections **\*\***Service endpoints **\*\***Azure Content Delivery Network **\*\***Path mapping | Custom domain names Nonpublic certificates and TLS/SSL settings Scale settings Always On IP restrictions WebJobs schedulers Diagnostic settings Cross-origin resource sharing (CORS) Virtual network integration Managed identities  
|

**\*** Setting can be configured to be slot-specific.

**\*\*** Feature isn't currently available.