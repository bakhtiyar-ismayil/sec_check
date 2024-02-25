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

Ensure that OpenSCAP is installed on your RHEL 8 system. You can install it using the following command:

* Select a Benchmark:

Choose the benchmark that you want to audit against. OpenSCAP supports various benchmarks such as those provided by DISA STIG, PCI-DSS, and CIS. You can find these benchmarks in the /usr/share/xml/scap/ssg/content directory.

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

* Run a Scan:
Use the oscap command-line tool to run a scan against the selected benchmark. For example, to scan against the PCI-DSS benchmark, you can use the following command:

```
oscap xccdf eval  --profile xccdf_org.ssgproject.content_profile_cis  --results-arf arf.xml  --report report.html /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml
```

The oscap xccdf generate fix command in OpenSCAP is used to generate remediation scripts or playbooks to fix security vulnerabilities identified during a compliance scan. In your command, you are specifying the use of Ansible as the fix type and providing various parameters to generate an Ansible playbook. Let's break down your command:

oscap xccdf generate fix: This initiates the process of generating a fix for identified vulnerabilities.

--fix-type ansible: Specifies that you want to generate an Ansible playbook as the fix.

--output playbook-rhel8.yml: Specifies the name of the output file where the generated Ansible playbook will be saved. In this case, it's playbook-rhel8.yml.

--result-id "xccdf_org.open-scap_testresult_xccdf_org.ssgproject.content_profile_cis": Specifies the result ID of the scan result to be used for generating the fix. This ensures that the fix is generated based on the results of a specific scan.

--fetch-remote-resources: Specifies that remote resources referenced in the scan result (such as OVAL definitions) should be fetched during the fix generation process.

arf.xml: Specifies the ARF (Asset Reporting Format) file containing the scan results.

It's worth noting that in your command, you haven't specified the SCAP content file (ssg-rhel8-ds.xml), which contains the benchmark against which the scan was performed. You may need to include this file if it's required for generating the fix.

Also, ensure that the ARF file specified (arf.xml) exists and contains the scan results. Adjust the paths and filenames as necessary to match your specific setup.

```
oscap xccdf generate fix --fix-type ansible --output playbook-rhel8.yml --result-id "xccdf_org.open-scap_testresult_xccdf_org.ssgproject.content_profile_cis" --fetch-remote-resources  arf.xml
```
