= Kiali cross-namespace validations of Istio rules.

The goal of this demo is to show Kiali's cross-namespace validation functionality in using the 'exportTo' field of Istio rules.
'exportTo' field can have  the values of namespaces where this rule is exported.
Also there are reserved values such as "." for exporting to own namespace only, and "\*" for exporting to all namespaces.
Not set value meand by default exported to all namespaces.

== Preconditions

It needs to have installed Istio and Kiali latest releases.
Also to have created 'bookinfo', 'bookinfo2' and 'bookinfo3' namespaces with bookinfo apps from https://github.com/istio/istio/tree/master/samples/bookinfo.

== Demo content

This demo is showing 2 different behaviors of the same cross-namespace validations, one in case when Istio rule is exported correctly and is used in validation, thus the message is shown with appropriate reference, and the second one is when export is done to other namespace and is not used in local object's validations.

=== Virtual Services

==== KIA1106 More than one Virtual Service for same host

In a case of showing cross-namespace validation warning, create the following objects.

[source,yaml]
----
kubectl apply -f virtual-service-host-exported.yaml
----

In a case when export is done into different namespace and cross-namespace validation is not done, create the following objects.

[source,yaml]
----
kubectl apply -f virtual-service-subset-presence-exported-not-match.yaml
----

==== KIA1107 Subset not found

In a case of showing cross-namespace validation warning, create the following objects.

[source,yaml]
----
kubectl apply -f virtual-service-subset-presence-exported.yaml
----

In a case when export is done into different namespace and cross-namespace validation is not done, create the following objects.

[source,yaml]
----
kubectl apply -f virtual-service-subset-presence-exported-not-match.yaml
----

== Destination Rules

=== KIA0201 More than one DestinationRules for the same host subset combination

In a case of showing cross-namespace validation warning, create the following objects.

[source,yaml]
----
kubectl apply -f dest-rule-host-subset-exported.yaml
----

In a case when export is done into different namespace and cross-namespace validation is not done, create the following objects.

[source,yaml]
----
kubectl apply -f dest-rule-host-subset-exported-not-match.yaml
----




