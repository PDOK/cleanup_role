[![GitHub license](https://img.shields.io/github/license/PDOK/cleanup_role)](https://github.com/PDOK/cleanup_role/blob/main/LICENSE)
[![GitHub release](https://img.shields.io/github/release/PDOK/cleanup_role.svg)](https://github.com/PDOK/cleanup_role/releases)

# Cleanup

An ansible role that will add ReplicaSets as ownerReferences to ConfigMaps. 
This is in order to make sure that generated ConfigMaps are deleted when there are no more ReplicaSets that use it.

## Requirements

This role uses the k8s and k8s_info modules.
These requires:
- openshift >= 0.8.0

## Role Variables

- resource: the custom resource needed to make sure that always an ownerRefernce exists on a configmap.
- replicaset_labels: an dictionary containing the labels that have been set on the replicaSets that are to be used for new ownerReferences.
- configmaps: a list of the complete generated configmaps so the ownerReferences can be added to them without changing anything else.

## Example Playbook

    - import_role:
        name: "../../roles/cleanup"
      vars:
        resource: "{{ _apiverison_kind }}"
        replicaset_labels: "{{ labels }}"
        configmaps:
        - "{{configmap_1}}"
        - "{{configmap_2}}"
