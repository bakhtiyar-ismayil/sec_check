# Lynis

Installation:


First, ensure that Lynis is installed on your system. You can download Lynis from its official website or install it via a package manager if available for your distribution.


```
sudo apt install lynis -y
```

```
sudo lynis audit system
```

# Open-Scap
```
yum install openscap-scanner scap-security-guide bzip2 -y
```

```
yum install scap-workbench
```
(if you use GUI)

```
oscap info /usr/share/xml/scap/ssg/content/ssg-rhel8-oval.xml
```
```
oscap info /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml  --profile xccdf_org.ssgproject.content_profile_cis
```

```
oscap xccdf eval  --profile xccdf_org.ssgproject.content_profile_cis  --results-arf arf.xml  --report report.html /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml
```


```
oscap xccdf generate fix --fix-type ansible --output playbook-rhel8.yml --result-id "xccdf_org.open-scap_testresult_xccdf_org.ssgproject.content_profile_cis" --fetch-remote-resources  arf.xml
```
