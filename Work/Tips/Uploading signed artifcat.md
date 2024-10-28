After upgrading or adding a dependency, to fix the error with `verifyAllSignatures` you probably need to upload it to the `signedthirdpartymaven` repository with the help of this job:

https://jenkins-engineering.dev.box.net/job/ArtifactSigning/job/gradle-sign-publish-dependencies

### See Also
- https://confluence.inside-box.net/pages/viewpage.action?spaceKey=ETO&title=Signing+And+Signature+Verification+Troubleshooting+Guide