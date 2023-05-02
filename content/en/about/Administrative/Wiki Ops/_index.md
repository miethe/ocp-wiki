+++
title = "Wiki Ops"
weight = 1
description = '''
How do I do cool formatting?
'''
+++

Below you will find example capabilities from Markdown, Hugo, and/or Docsy.

## Docsy
You can find more info on the below [here](https://www.docsy.dev/docs/adding-content/shortcodes/).

### Shortcodes

#### Blocks/Lead

{{% blocks/lead color="primary" %}}
&nbsp;

TechOS is the OS of the future.

Runs on **bare metal** in the **cloud**!

&nbsp;
{{% /blocks/lead %}}

#### Blocks/Section
{{< blocks/section color="secondary" >}}
{{% blocks/feature icon="fa-lightbulb" title="Fastest OS **on the planet**!" %}}
The new **TechOS** operating system is an open source project. It is a new project, but with grand ambitions.
Please follow this space for updates!
{{% /blocks/feature %}}
{{% blocks/feature icon="fa-brands fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" %}}
We do a Pull Request contributions workflow on **GitHub**. New users are always welcome! 
{{% /blocks/feature %}}
{{% blocks/feature icon="fa-brands fa-twitter" title="Follow us on Twitter!" url="https://twitter.com/GoHugoIO" %}}
For announcement of latest features etc.
{{% /blocks/feature %}}
{{< /blocks/section >}}

#### Blocks/Feature
{{% blocks/feature icon="fa-brands fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" %}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{% /blocks/feature %}}

#### Blocks/Link-down
{{% blocks/lead color="primary" %}}
    Go to next Section: {{< blocks/link-down color="info" >}}
{{% /blocks/lead %}}

### Shortcode Helpers

#### Alert
{{% alert title="Warning" color="warning" %}}
This is a warning.
{{% /alert %}}

#### Pageinfo
{{% pageinfo color="primary" %}}
This is placeholder content.
{{% /pageinfo %}}

#### Boxes

{{< box info >}}
  Test info box
{{< /box >}}

{{< box warning >}}
  Test warning box
{{< /box >}}

{{< box tip >}}
  Test tip box
{{< /box >}}

{{< box important >}}
  Test important box
{{< /box >}}

#### GitHub API

{{< github-api url="https://api.github.com/users/miethe/starred?per_page=3" >}}

#### iframe
[iframes](https://www.w3schools.com/tags/tag_iframe.asp)

#### Details
{{< details title="More info inside here.">}}
{{< youtube-sm id="5Rsr70b342s" title="OCM - Ctrl Plane and ClusterAPI Demo" >}}
{{< /details >}}

#### Tabbed Panes
{{< tabpane text=true right=true >}}
  {{% tab header="**Languages**:" disabled=true /%}}
  {{% tab header="English" lang="en" %}}
  ![Flag United Kingdom](flags/uk.png)
  Welcome!
  {{% /tab %}}
  {{< tab header="German" lang="de" >}}
    <b>Herzlich willkommen!</b>
    <img src="flags/de.png" alt="Flag Germany" style="float: right; padding: 0 0 0 0px">
  {{< /tab >}}
  {{% tab header="Swahili" lang="sw" %}}
  ![Flag Tanzania](flags/tz.png)
  **Karibu sana!**
  {{% /tab %}}
{{< /tabpane >}}

#### Cards
{{< card header="**Imagine**" title="Artist and songwriter: John Lennon" subtitle="Co-writer: Yoko Ono"
          footer="![SignatureJohnLennon](https://server.tld/…/signature.png 'Signature John Lennon')">}}
Imagine there's no heaven, It's easy if you try<br/>
No hell below us, above us only sky<br/>
Imagine all the people living for today…
{{< /card >}}

#### Card-code
{{< card-code header="**C**" lang="C" >}}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  puts("Hello World!");
  return EXIT_SUCCESS;
}
{{< /card-code >}}

#### Card groups
{{< cardpane >}}
  {{< card header="Header card 1" >}}
    Content card 1
  {{< /card >}}
  {{< card header="Header card 2" >}}
    Content card 2
  {{< /card >}}
  {{< card header="Header card 3" >}}
    Content card 3
  {{< /card >}}
{{< /cardpane >}}