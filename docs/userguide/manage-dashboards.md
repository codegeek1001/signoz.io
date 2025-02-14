---
id: manage-dashboards
title: Manage Dashboards
sidebar_label: Manage Dashboards
---

import GetHelp from '../shared/get-help.md'

This section shows how you can create, update, and remove dashboards.

:::tip

We have shared some commonly used dashboard JSON files [here](https://github.com/SigNoz/dashboards). You can import them directly to create dashboards in SigNoz.

:::

## Create a Custom Dashboard

1. From the sidebar, choose **Dashboards**.
2. Select the **New Dashboard** button.
3. Select the **Edit** button at the far right, and then enter the following information:
    1. A descriptive name for your new dashboard.
    2. *(Optional)* Add one ore more tags by selecting the **New Tag** button.
    3. *(Optional)* A brief description of your new dashboard.

4. Select the **Save** button at the far right.

5. For each panel you wish to add to your new dashboard, follow the steps in the [Add a Panel to a Dashboard](/docs/userguide/manage-panels#add-a-panel-to-a-dashboard) section.

6. *(Optional)* You can change the order of your panels by dragging and dropping them.

7. When you’ve finished, select the **Save Layout** button.


## Update a Custom Dashboard

To update the name, description and tags:

1. Select the **Edit** button at the far right.
2. Make the changes.
3. Select the **Save Layout** button.

To resize a panel:

1. Click the bottom-left corner of the panel you want to resize.
2. Keep your left mouse button pressed and resize the panel.
3. When you've finished, select the **Save Layout** button.

To change the position of a panel:

1. Drag and drop a panel to the new position.
2. When you’ve finished, select the **Save Layout** button.


## Remove a Custom Dashboard

1. From the sidebar, choose **Dashboard**.
2. Find the dashboard you wish to remove. In the **Action** column, select the **Delete** button.

## Import a Grafana dashboard

Status: Experimental


In [0.11.3](https://github.com/SigNoz/signoz/releases/tag/v0.11.3) release, we have added the ability to import Grafana dashboards. It currently supports importing via JSON and Prometheus as a supported data source. This allows you to easily import any of your pre-existing infrastructure or application metrics dashboards into SigNoz. All the relevant meta and format info, such as Y-axis, legend formatting, etc., is also preserved and transformed to make it work in SigNoz dashboards.

To import the Grafana dashboard:


1. From the sidebar, choose **Dashboards**.
2. Select the **New Dashboard** button.
3. Select the **Import Grafana JSON** option, and then you are given two options

    1. Upload JSON File
    2. Paste JSON below
4. Import the JSON with one of the suggested methods
5. Confirm using the **Load JSON** button on the bottom left.

Once the above steps are completed successfully, you will see a new dashboard, and if there is data matching the PromQL queries, it should work right away.

Note: The imported dashboard might have the variables, and those variables are copied as is from the source. The query type ones do not work since SigNoz supports variable by query using ClickHouse. You might have to update them. Please follow [this](./manage-variables.md) guide for more info.


## Get Help

<GetHelp />
