# Angular Style Guide Change and Suffix Drop

In 2024 Angular team has decided to refresh the styleguide for the framework and with that refresh introduce couple convention-breaking changes. 
These changes were officially implemented in 2025. 

The most controversial one was the following: 

>  ## Stop recommending suffixing most file names and class names with the type of construct
>  The current style guide recommends suffixing file names and class names with the type of Angular
>  construct. For example:
>
>  `user-profile.component.ts` and `UserProfileComponent`
> 
>  `campaign-data.service.ts` and `CampaignDataService`
>
>  Over time, we've observed that this naming convention can make the framework feel cumbersome and
>  boilerplate-y, especially for new developers unaccustomed to this practice.


Namely, the files named `User.component.ts` would now be named `User.ts` and `User.service.ts` would also be named `User.ts`.
That would be a conflict if they'd be in the same directory, and the new official recommendation is for the old `User.service.ts` 
to be renamed into `UserApiClient.ts` or whatever its actual function is. 

As many have indicated in the thread at https://github.com/angular/angular/discussions/58412 
this change apparently aimed at newcomers who supposedly feel the framework to be "cumbersone and boilerplate-y" 
absolutely destroys a set of long-standing angular conventions and good practices that were essential in maintaining large codebases with complex structures 
where a given entity `User` used to have a separate file for the
- component
- model
- service

sometimes more, all with clearly defined suffixes in the file name, but also in the class name defined inside.

Removing the suffixes would not only remove the clear file naming convention, crucial to maintaining large-scale projects, but also
- Break Prettier detection of Angular components, see https://github.com/angular/angular/discussions/58412#discussioncomment-11091293
- Break VSCode detection of file types that allows to apply icons 
- Break any IDE file-finding features depending on the file name suffix to differentiate various files relating to the same entity

All indicated by many, who raised issues around the changes significantly worsening the Developer Experience
- https://github.com/angular/angular/discussions/58412#discussioncomment-11114913
- https://github.com/angular/angular/discussions/58412#discussioncomment-11104776
- https://github.com/angular/angular/discussions/58412#discussioncomment-11105769
- https://github.com/angular/angular/discussions/58412#discussioncomment-11156337
- https://github.com/angular/angular/discussions/58412#discussioncomment-11158639
- https://github.com/angular/angular/discussions/58412#discussioncomment-11186429
- https://github.com/angular/angular/discussions/58412#discussioncomment-11204355
- https://github.com/angular/angular/discussions/58412#discussioncomment-11211596

Regardless of the feedback (most of it was about opposing the suffix removal), 
the change went through and suffixes are disabled in new projects by default, 
BUT can still be configured back. 

To create an app with the suffixes on filenames enabled, you can: 
- Create it with `ng new <AppName> --file-name-style-guide=2016`

But that will not enable the classname suffixes, only filename suffixes. 

To enable the classname suffixes you will also have to go into `angular.json`
file and ensure you have `"addTypeToClassName": true` set in your schematics, like this: 

```
"@schematics/angular:component": {
  "style": "scss",
  "type": "component",
  "addTypeToClassName": true
},
"@schematics/angular:directive": {
  "type": "directive",
  "addTypeToClassName": true
},
"@schematics/angular:service": {
  "type": "service",
  "addTypeToClassName": true
},
```
