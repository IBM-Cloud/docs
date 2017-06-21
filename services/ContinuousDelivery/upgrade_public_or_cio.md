---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrading IBM Confidential projects to toolchains 
{: #upgrade_public_or_cio}

{{site.data.keyword.jazzhub}} is evolving into IBM Bluemix {{site.data.keyword.contdelivery_short}}. As part of that change, projects will be upgraded to toolchains.

When your project is ready to be upgraded, a message is displayed on its Overview page. You can then upgrade the project to a toolchain on {{site.data.keyword.Bluemix_notm}} Public. The toolchain will include a Whitewater {{site.data.keyword.ghe_short}} repository (repo) for your source code. Whitewater {{site.data.keyword.ghe_short}} is provided to IBM teams to promote and enable social coding within IBM. 
{: shortdesc}

**{{site.data.keyword.contdelivery_short}} toolchains are approved for IBM Confidential material when they are used with Whitewater {{site.data.keyword.ghe_short}}.** Delivery Pipelines that receive input from Whitewater {{site.data.keyword.ghe_short}} repos can deploy to staging (YS1) and public (YP) environments.

During the upgrade, you will be prompted to authorize {{site.data.keyword.contdelivery_short}} to access Whitewater {{site.data.keyword.ghe_short}} on your behalf.

## Adding members to your Whitewater {{site.data.keyword.ghe_short}} repo after the upgrade

If your project uses a repo that is hosted on JazzHub, during the upgrade a new repo is created on Whitewater {{site.data.keyword.ghe_short}}. After the upgrade, the person who started the upgrade must add team members to the Whitewater {{site.data.keyword.ghe_short}} repo and ensure that they have the correct privileges before they can access the new repo.

## Troubleshooting

An intermittent problem sometimes occurs when you try to change the target of a pipeline deployment stage. When this problem happens, an error is shown in the **Organization** and **Space** fields.

This problem typically occurs only when you change the target from the pipeline so that the pipeline that is created during the upgrade will deploy correctly to the same targets as it did before.

If you try to change the target and this problem occurs, switch between targets a few times until the **Organization** and **Space** fields are filled in.

A related problem occasionally causes deploys to YS1 targets to fail. This situation is rare; if it happens, re-run the pipeline.

The IBM DevOps Services team is actively working to resolve these problems.
