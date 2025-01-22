---
{"dg-publish":true,"permalink":"/how-i-publish-my-obsidian-vault-for-free-using-digital-garden-plugin/","tags":["tutorial"],"noteIcon":"1","created":"2025-01-03T19:50:02.722+08:00","updated":"2025-01-23T01:24:52.470+08:00"}
---

Follow this tutorial if you want to publish your obsidian vault just like mine. This method is highly customizable. It supports other Obsidian plugins such as Excalidraw and Dataview.

> [!info]- Alternative publishing: Quartz
> I used to publish my Obsidian Vault using Quartz. However, it does not support Dataview plugin and the site can easily break if you did a lot of customization. Quartz is more of a framework. If you prefer simple setup with a clean layout, you can refer to this [[How I Publish My Obsidian Vault For Free Using Quartz\|tutorial]].


# Tools
1)  [Obsidian](https://obsidian.md/) - Of course, for note-taking.
2) [Cloudflare Pages](https://pages.cloudflare.com/) - For hosting static-generated site.
3) A domain name. I purchase my domain name through [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/), because the price of the domain maintain the same for the following year.
4) [Digital Garden Plugin](https://github.com/oleeskild/obsidian-digital-garden) - Install the community plugin. The [docs](https://dg-docs.ole.dev/) provides useful resources on how to setup and modify the site.
5) [Github Account](https://github.com/) - To create a repository. It can be private or public.

> [!note]+
> You can use different hosting, such as using Netlify instead of Cloudflare Pages. Refer to the official documentation [here](https://dg-docs.ole.dev/advanced/hosting-alternatives/). This guide will use the tools as I listed.
# Getting Started
**Step 1:**
Choose an Obsidian vault or create a new one. Make sure to install and enable the Digital Garden plugin.  Go to settings > Community plugins > browse > "Digital Garden".
![Pasted image 20250109222549.png](/img/user/assets/Pasted%20image%2020250109222549.png)

**Step 2:**
Login to your Github account. Go to this [repository](https://github.com/oleeskild/digitalgarden) and click the "use this template" button. Then, click "Create a new repository". Create your repository by filling in the repository name and set it to either public or private.
![dg_s2.png](/img/user/assets/dg_s2.png)