# Zotero Addons Scraper

This is a script repository for scraping Zotero addon collections for [Zotero7+](https://www.zotero.org), intended for use with [Zotero addons](https://github.com/syt2/zotero-addons).
*Switch to GitHub(backup) source in [Zotero addons](https://github.com/syt2/zotero-addons) to use this repository.*

The script utilizes the GitHub API and GitHub Actions to automatically scrape, parse, and publish corresponding addon information from the [addons](addons) file to the latest release.

## Contributing New Addons
If you have a new add-on to parse, add the json information of the add-on in the [addons](addons) folder with the format 
``` json
{
  "id": "zoteroAddons@ytshen.com",
  "name": "Zotero 插件合集",
  "repo": "syt2/zotero-addons",
  "releases": [
    {
      "targetZoteroVersion": "7",
      "tagName": "latest"
    }
  ]
}
```

## Addon Information Format

The output format for add-on information follows the format specified in [zotero-chinese/zotero-plugins](https://github.com/zotero-chinese/zotero-plugins), which is as follows:
```ts
export interface PluginInfo {
  /**
   * 插件名称
   */
  name: string;
  /**
   * 插件仓库
   *
   * 例如：northword/zotero-format-metadata
   *
   * 注意前后均无 `/`
   */
  repo: string;
  /**
   * 插件的发布地址信息
   */
  releases: Array<{
    /**
     * 当前发布版对应的 Zotero 版本
     */
    targetZoteroVersion: string;
    /**
     * 当前发布版对应的下载通道
     *
     * `latest`：最新正式发布；
     * `pre`：最新预发布；
     * `string`：发布对应的 `git.tag_name`；
     * 注意 `git.tag_name` 有的有 `v` 而有的没有，可以通过发布链接来判断
     */
    tagName: "latest" | "pre" | string;

    currentVersion?: string;
    xpiDownloadUrl?: {
      github: string;
      gitee: string;
      ghProxy: string;
      jsdeliver: string;
      kgithub: string;
    };
    releaseData?: string;
    downloadCount?: number;
    assetId?: number;
  }>;

  description?: string;
  star?: number;
  author?: {
    name: string;
    url: string;
    avatar: string;
  };
}
```