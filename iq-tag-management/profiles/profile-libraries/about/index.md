---
title: About profile libraries
description: This article describes profile libraries in iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/profiles/profile-libraries/about/
---
## How it works

Libraries are used to manage configurations that are shared across multiple profiles. Consider the following points before you begin working with libraries:

* A profile can load one or more libraries, but libraries cannot load profiles or other libraries.
* A library is almost identical to a profile with the exception that a library can be imported into another profile.
* After an element from a library is imported into a profile, it cannot be edited.
* You can modify the tag configuration of an imported tag, as changes to tag configuration take precedence over library settings.
* After saving and publishing a profile with imported libraries, the resulting version and `utag.js` file represent the entire profile configuration.

## Identify library elements in a profile

Consider the following when identifying library elements in a profile:

* Elements added from a library receive a label that indicates which library each element belong to.
* Tags added to a profile through a library receive a unique ID for that profile. This unique ID may be different than the ID that a tag receives when added to the library.
* Any tag, load rule, or extension added in a library will display as **ON** in the profile that loads the library. You cannot turn off a library-loaded element from a profile that loads the library.
* You cannot remove data layer variables imported from a library.
