# AutoUpdater

This is the basic sample of JSON Format uploaded in your hosting site.

- File name **e.g.:** **_latest-update.json_**
- File content

```json
{
  "name": "AutoUpdater",
  "version": "0.1.2",
  "descriptions": "This is the latest update."
}
```

Deserialize the Json object.

```C#
	//Get the app current version
	var current = Assembly.GetExecutingAssembly().GetName().Version;
	using (var sr = new StreamReader(stream))
	{
		var result = sr.ReadToEnd();

		//Deserialize Object to ApplicationsInfo
		var appInfo = JsonConvert.DeserializeObject<ApplicationInfo>(result);
		var app = Version.Parse(appInfo.Version);
		var versionResult = version.CompareTo(current);

		//check new version available
		if (versionResult > 0)
		{
			DownloadUpdate(app.DownloadUrl);
		}
		else
		{
			ChangeStats("No updates available.");
		}
	}


	public class ApplicationInfo
	{
		public string Name { get; set; }
		public string Version { get; set; }
		public string Descriptions { get; set; }
		public string DownloadUrl { get; set; }
	}
```
