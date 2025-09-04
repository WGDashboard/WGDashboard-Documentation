# 📣 What's New: v4.3.0

<img src="https://wgdashboard-resources.tor1.cdn.digitaloceanspaces.com/Releases/v4.3.0.png" style="block"  alt="" />

It has been more than 5 months since our last release, and we are happy to announce our next version with more exciting features!

## 🔥 Breaking News

- We've moved the WGDashboard project from my personal GitHub to the [WGDashboard Organization](https://github.com/WGDashboard)! If you wish, please give us a follow, thank you so much ❤️
- A new **Client** side dashboard is available, where clients can sign in to view WireGuard Peers assigned to them. For more information, please visit: [](Client-Side-Dashboard.md) ([#720](https://github.com/WGDashboard/WGDashboard/issues/720))
- Plugins are now available for developers who want to extend the use of WGDashboard, for more information, please visit: [](WGDashboard-Plugins.md). **Note: This feature is still under experiment but is available to use**

## 🎉 New Features
- With replacing `sqlite3` with `sqlalchemy` in the Python codes, we are now officially support using **SQLite**, **PostgreSQL** or **MySQL** for WGDashboard's database. For more information, please visit [](✂️-Dashboard-Configuration.md#database) ([#734](https://github.com/WGDashboard/WGDashboard/issues/734))
- You can now set up webhooks to run after peers **created, deleted & updated**. For more information, please visit: [Webhooks](Webhooks.md) ([#669](https://github.com/WGDashboard/WGDashboard/issues/669))
- Custom headers when connect to **Cross Server** ([#491](https://github.com/WGDashboard/WGDashboard/issues/491))
- Historical network usage and sessions for peers are now available under **Details** for each peer ([#620](https://github.com/WGDashboard/WGDashboard/issues/620))
- Added Jinja template in Peer Default Settings ([#843](https://github.com/WGDashboard/WGDashboard/issues/843))
- Grouping peers with tags and filter in the UI ([#355](https://github.com/WGDashboard/WGDashboard/issues/355))
- Override Peer Default Settings within configuration. Let's say if your configuration is on `ip_address:51820` but you want them connect through port `51234` just for `wg0`, you can now do so. ([#682](https://github.com/WGDashboard/WGDashboard/issues/682)， [#630](https://github.com/WGDashboard/WGDashboard/issues/630))

## 🛠️ Adjustments
- Added support to Debian 13 ([#858](https://github.com/WGDashboard/WGDashboard/issues/858))
- **MTU** is no longer required when adding new peers ([#564](https://github.com/WGDashboard/WGDashboard/issues/564))
- Configuration list in navigation bar now sync the order with the ones in homepage ([#841](https://github.com/WGDashboard/WGDashboard/issues/841))
- Peers dropdown menu will not go overflow if it touch the bottom of the screen ([#644](https://github.com/WGDashboard/WGDashboard/issues/644))

## 🧐 Bugs Fixed
- Configuration network traffic graph is incorrect ([#854](https://github.com/WGDashboard/WGDashboard/issues/854))
- When using `app_prefix`, locale is not fetch properly in Docker environment ([#853](https://github.com/WGDashboard/WGDashboard/issues/853))