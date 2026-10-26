# calopsys\.containers Release Notes

**Topics**

- <a href="#v1-3-0">v1\.3\.0</a>
    - <a href="#minor-changes">Minor Changes</a>
    - <a href="#breaking-changes">Breaking Changes</a>
    - <a href="#bugfixes">Bugfixes</a>
- <a href="#v1-2-0">v1\.2\.0</a>
    - <a href="#release-summary">Release Summary</a>
    - <a href="#major-changes">Major Changes</a>
- <a href="#v1-1-0">v1\.1\.0</a>
    - <a href="#release-summary-1">Release Summary</a>
    - <a href="#major-changes-1">Major Changes</a>
- <a href="#v1-0-0">v1\.0\.0</a>

<a id="v1-3-0"></a>
## v1\.3\.0

<a id="minor-changes"></a>
### Minor Changes

* podman \- added the variable <code>calopsys\_podman\_application\_rollback\_enabled</code>\. When a deployment fails\, the role restores the previous application directory\.
* podman \- added the variables <code>calopsys\_podman\_application\_directories</code> and <code>calopsys\_podman\_application\_files</code> to create application directories and files\.
* podman \- added the variables <code>calopsys\_podman\_application\_restart\_policy</code> and <code>calopsys\_podman\_application\_timeout</code>\.
* podman \- added the variables <code>calopsys\_podman\_compose\_deb\_url</code> and <code>calopsys\_podman\_compose\_deb\_checksum</code> to set an alternative package source\.
* podman \- the role installs podman\-compose version <code>calopsys\_podman\_compose\_version</code> \(default <code>1\.6\.0\-1</code>\) from snapshot\.debian\.org instead of the Debian repository\. The hosts must have access to snapshot\.debian\.org\, or you must set <code>calopsys\_podman\_compose\_deb\_url</code>\.
* podman \- the systemd ExecStart script fails when compose declares more services than it created\.
* podman \- the systemd unit starts the application with an ExecStart script\. The script waits until all containers are healthy\.
* podman \- the systemd unit stops the application with <code>podman\-compose stop</code> in <code>ExecStop</code> and <code>podman\-compose down</code> in <code>ExecStopPost</code>\.

<a id="breaking-changes"></a>
### Breaking Changes

* podman \- the role removed the variable <code>calopsys\_podman\_application\_sdnotify</code>\.
* podman \- the role replaced <code>tasks/compose\.yml</code> with <code>tasks/application\.yml</code>\. Change <code>tasks\_from\: compose\.yml</code> to <code>tasks\_from\: application\.yml</code>\.

<a id="bugfixes"></a>
### Bugfixes

* podman \- <code>podman\_login</code> stores the auth file in <code>\~/\.config/containers/auth\.json</code> instead of <code>\$XDG\_RUNTIME\_DIR</code>\. Registry logins now persist after a reboot\.

<a id="v1-2-0"></a>
## v1\.2\.0

<a id="release-summary"></a>
### Release Summary

Release Date\: 2026\-02\-26

<a id="major-changes"></a>
### Major Changes

* ci \- moved to lima molecule driver \([https\://github\.com/calopsys/ansible\-collection\-containers/pull/5](https\://github\.com/calopsys/ansible\-collection\-containers/pull/5)\)

<a id="v1-1-0"></a>
## v1\.1\.0

<a id="release-summary-1"></a>
### Release Summary

Release Date\: 2026\-02\-26

<a id="major-changes-1"></a>
### Major Changes

* ci \- moved to vagrant molecule driver \([https\://github\.com/calopsys/ansible\-collection\-containers/pull/2](https\://github\.com/calopsys/ansible\-collection\-containers/pull/2)\)
* roles \- added podman role and ci \([https\://github\.com/calopsys/ansible\-collection\-containers/pull/3](https\://github\.com/calopsys/ansible\-collection\-containers/pull/3)\)

<a id="v1-0-0"></a>
## v1\.0\.0

