---
title: "Atlas Artifact Provider"
---
# Atlas Artifact Provider

Terraform has a [provider](https://terraform.io/docs/providers/index.html) for managing Atlas artifacts called `atlas_artifact`.

This is used to make data stored in Atlas Artifacts available to
Terraform for interpolation. In the following example, an artifact
is defined and references an AMI ID stored in Atlas.

    provider "atlas" {
      # You can also set the atlas token by exporting
      # ATLAS_TOKEN into your env
      token = "${var.atlas_token}"
    }

    resource "atlas_artifact" "web-worker" {
      name = "acmeinc/web-worker"
      type = "amazon.image"
      version = "latest"
    }

    resource "aws_instance" "worker-machine" {
      ami = "${atlas_artifact.web-worker.metadata_full.region-us-east-1}"
      instance_type = "m1.small"
    }

This automatically pulls the "latest" artifact version.

Following a new artifact version being created via a Packer build, the following
diff would be generated when running `terraform plan`.

    -/+ aws_instance.worker-machine
        ami:             "ami-168f9d7e" => "ami-2f3a9df2" (forces new resource)
        instance_type:   "m1.small" => "m1.small"

This allows you to reference changing artifacts and trigger new deployments
upon pushing subsequent Packer builds.

Read more about artifacts in the [Terraform documentation](https://terraform.io/docs/providers/atlas/r/artifact.html).
