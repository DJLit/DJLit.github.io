# DJ Lit's documentation of everything tech!
## For teams after 2019-20

Hello! If you're looking at this, it's because you wish to understand how we've built the various services and websites in DJ Lit. In college, I bet my ass that no other committee/ club documents as much as I'm going. Before I start, this documentation is going to be really long. However, feel free to jump to the sections that you require anytime.

### Services

In the committee, we provite the following tech services:

1. DJVU ([djvu.in](https://www.djvu.in))

DJVU is the blogging platform of the committee. Every editorial member has an account, and the tech head has an account. Tech team can be given accounts if need be. I will explain the entire website in a later section.

2. Email (something@djvu.in)

If any outsider wishes to contribute their article to the blog, they can do so by sending an email to this email address. However, this is only a redirector! It's not an actual inbox. More on this in a specific section.

### History of DJVU

DJVU is the publication platform of DJ Lit. Started off as a wordpress website for college news and updates, DJVU has now pivotted to a blogging platform for all students in college.

DJVU started off in 2015/16 as a wordpress website however there were many problems:
- The theme in use was not good looking
- The website was slow and clumsy
- Very confusing layout
- Very confusing admin panel

The website was, in Vikrant's opinion, a bad shape. Hence, the wordpress website was migrated to Ghost CMS - a NodeJS based blogging platform.
Ghost has proven to be much faster than wordpress, bringing down the loading time from 17s to 7s.
Furthermore, with Cloudflare CDN, HTTP/2, and caching, the site performance has improved even more.

Reason why we shifted to Ghost in 2019-20:
- Fast performance
- Speed = better SEO results
- Better SEO overall
- Good looking theme
- Beautiful admin panel

### Technology Stack

- GoDaddy for hosting (Linux, shared cPanel hosting)
- GoDaddy for domain name
- Cloudflare for SSL and DNS
- Ghost CMS for application
- PM2 for process management

### Caveats

Even though we shifted to Ghost, Ghost is a little bit difficult to develop on. Developing theme and pages is quite difficult. This is because
of Handlebars and lack of wordpress-like GUI tools for theme customization. More problems:
- Hosting NodeJS on GoDaddy was difficult
- Setting up Ghost on shared hosting was difficult
- Theme customization is difficult because Ghost prefers headless mode like Gatsby websites
- Handlebars is difficult

Hence, in future, **if committee wants to shift to wordpress again, you can contact Vikrant for guidance on how to migrate the database.**
Setting up wordpress is not difficult. It's only the question of extracting data from Ghost's sqlite database and adding that to
wordpress's MySQL database, which isn't as difficult.

### Hosting

As mentioned, we use GoDaddy for hosting a NodeJS site. If you search online, everyone will say its impossible. However we did it anyways. Here's how:
- Install NVM. NVM allows you to install node without a package manager
- Install Ghost CLI
- Make a ghost blog
- Start ghost blog
- Add .htaccess to redirect requests to node process's port

All this has to be done using SSH.

### Process management

Because of the _jugaad_ mentioned above in the hosting section, the Ghost process exits from time to time. Hence, we use PM2 for automatic restarts.
However, using PM2 means we can't use ghost cli. Hence we copy the config file and pm2 environment file from one ghost version to other.
Since Ghost is a node project, there is an index.js file which you can run with pm2.

### Security

We did not buy an SSL certificate. Doesn't matter, we use Cloudflare for that.
In GoDaddy DNS settings, change the nameservers to Cloudflare and import the domain into Cloudflare DNS.
Once done, settup flexible SSL and automatic HTTPS redirects.

### What to do if site goes down

Often Ghost process exits due to the shitty GoDaddy hosting. If that happens,
- ssh into the server
- go to djvu_blog/ folder
- start ghost again using ghost-cli or pm2, preferably pm2

```bash
ssh <confidential information omitted>
cd djvu_blog
cd current
pm2 start ecosystem.config.yaml
```
