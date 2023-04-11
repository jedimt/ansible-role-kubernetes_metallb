Ansible Role: Kubernetes MetalLB
=========

Installs the MetalLB software load balancer in a Kubernetes cluster.

Requirements
------------

Functional Kubernetes cluster.

Role Variables
--------------

This role can install either the configmap based MetalLB v0.12.1 or the CRD based v0.13.x versions.

    # MetalLB L2 load balancer for K8s (v0.13.9 | v0.12.1)
    metallb_version: "v0.13.9"

    # For previous configmap based versions, v0.12.1 was last release
    # metallb_version: "v0.12.1"

    # "Service" IP addresses to use for pods needing a load balancer
    # This example represents a continuous range of five IP addresses
    metallb_start: 10.100.24.48
    metallb_end: 10.100.24.52

    # URL to pull MetalLB manifests for v0.13x versions
    metallb_v13_url: "https://raw.githubusercontent.com/metallb/metallb/{{ metallb_version }}/config/manifests"

    # URLs for MetalLB manifests for v0.12.x version
    metallb_v12_base_url: https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests
    metallb_v12_namespace_url: "{{ metallb_v12_base_url }}/namespace.yaml"
    metallb_v12_metallb_url: "{{ metallb_v12_base_url }}/metallb.yaml"

Dependencies
------------

None.

Example Playbook
----------------

    # ===========================================================================
    # Install MetalLB L2 load balancer
    # ===========================================================================
    - name: Install MetalLB load balancer
      hosts: k8s_master
      become: true

      roles:
        - jedimt.kubernetes_metallb

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
