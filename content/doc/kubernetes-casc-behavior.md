What I tested

Jenkins was started with CasC enabled.
The CasC YAML did not define any cloud configuration.

Case 1: Cloud with only a name

I added a Kubernetes cloud and only entered the name.
No other fields were set.

Result:
The cloud was still present after restarting Jenkins.

Reason:
The configuration is incomplete, so Jenkins does not fully save it.
Because of this, CasC does not actively remove it.
This looks like an edge case and not intended behavior.

Case 2: Cloud with invalid values

I added a Kubernetes cloud with some test or invalid values.

Result:
The cloud disappeared after restarting Jenkins.

Reason:
The cloud configuration is saved in Jenkins config, but it is not defined in the CasC YAML.
When Jenkins starts, CasC reloads its configuration and removes UI-only settings.

Case 3: Cloud with valid values

I added a Kubernetes cloud with valid values and confirmed the connection worked.

Result:
The cloud disappeared after restarting Jenkins.

Reason:
Same behavior as case 2.
CasC treats its YAML as the source of truth and removes any cloud not defined there.
The validity of the configuration does not matter.

Summary

When CasC is enabled, any Kubernetes cloud created through the UI is removed on restart unless it is defined in the CasC YAML.
There is no warning shown when this happens.
