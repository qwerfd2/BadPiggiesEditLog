# BadPiggiesEditLog捣蛋猪更改日志
The Edit log of my BP Hack - tools needed：DnSpy， Apktool， and JDK。需要的工具：DnSpy， Apktool， 和 JDK
-------------------
APK下载链接： 链接:[有效] https://pan.baidu.com/s/1obd74lw6-lIzv2Ib2Pswuw 提取码:9094复制这段内容后打开百度网盘手机App，操作更方便哦
Process map: Raw APK ---> Apktool unpack ---> assets/bin/Data/Managed/Assembly-CSharp.dll ---> edit & save via DnSpy --->Apktool pack ---> JDK keystore & jarsigner ---> hacked APK! 原版APK--->Apktool解包--->assets/bin/Data/Managed/Assembly-CSharp.dll--->用DnSpy更改保存--->Apktool压包--->JDK keystore & jarsigner ---> 破解APK!


Grid & Camera Zoom hack


		BaseGameMode.InitGameMode
		using System.Collections.Generic;
		using System.Linq;
		using UnityEngine.SceneManagement;
		if (Singleton<GameManager>.Instance.CurrentEpisodeType == GameManager.EpisodeType.Sandbox && WPFMonoBehaviour.levelManager.CurrentGameMode is BaseGameMode)
		{
			List<int> intList = new List<int>
			{
				4095,
				4095,
				4095,
				4095,
				4095,
				4095,
				4095,
				4095
			};
			base.CurrentConstructionGridRows = intList;
		}
		else
		{
			base.CurrentConstructionGridRows = this.levelManager.m_constructionGridRows;
		}
---------------------------------
LevelManager.CurrentConstructionGridRows
		
		
		get
		{
			if (Singleton<GameManager>.Instance.CurrentEpisodeType == GameManager.EpisodeType.Sandbox && WPFMonoBehaviour.levelManager.CurrentGameMode is BaseGameMode)
			{
				return new List<int>
				{
					4095,
					4095,
					4095,
					4095,
					4095,
					4095,
					4095,
					4095
				};
			}
			return this.m_gameMode.CurrentConstructionGridRows;
		}
------------------------------------------------
InGameCamera.Start
		
		
		if (Singleton<GameManager>.Instance.CurrentEpisodeType == GameManager.EpisodeType.Sandbox && WPFMonoBehaviour.levelManager.CurrentGameMode is BaseGameMode)
		{
			this.m_cameraBuildZoom = 7.5f;
		}
		else
		{
			this.m_cameraBuildZoom = this.m_cameraPreview.ControlPoints[this.m_cameraPreview.ControlPoints.Count - 1].zoom;
		}
----------------------------
SnoutCoin: 
 		
		
		public static void AddSnoutCoins(int count)
	{
		if (Singleton<BuildCustomizationLoader>.Instance.IsOdyssey)
		{
			return;
		}
		GameProgress.m_data.GetInt("SnoutCoins", 0);
		GameProgress.m_data.SetInt("SnoutCoins", 99999);
	}
  --------------------------
Scrap:
  	
	
	public static bool UseScrap(int amount)
	{
		int @int = GameProgress.m_data.GetInt("Scrap", 0);
		if (@int >= amount)
		{
  		//deleted amount -= @int
		GameProgress.m_data.SetInt("Scrap", @int);
		if (GameProgress.OnScrapAmountChanged != null)
		{
		GameProgress.OnScrapAmountChanged();
		}
		return true;
		}
		return false;
	}
  ---------------------
Powerups:
  
  
	public static int BluePrintCount()
	{
		return 99999;
	}
  // the same as all other Counts (supermagnets, glues, etc.)
  ---------
  Desert Count
 
 
 	public static int DessertCount(string dessertName)
	{
		return 9999;
	}
  -------------------------
Level3Star:
	
	
	public static int GetRaceLevelUnlockedStars()
	{
		return 3;
	}
	 // and

-----------
Unlock all level:
		
		public static bool AllLevelsUnlocked()
	{
		return true;
	}
  ----------------
  
Large amounts of parts:


 		GameProgress.InitializeGameProgressData //inserted in this method
		IEnumerator enumerator = Enum.GetValues(typeof(BasePart.PartType)).GetEnumerator();
		try
		{
			while (enumerator.MoveNext())
			{
				object obj = enumerator.Current;
				BasePart.PartType partType = (BasePart.PartType)obj;
				if (partType != BasePart.PartType.Unknown && partType != BasePart.PartType.ObsoleteWheel && partType != BasePart.PartType.JetEngine)
				{
					int sandboxPartCount = GameProgress.GetSandboxPartCount(partType);
					GameProgress.AddSandboxParts(partType, 99 - sandboxPartCount, false);
				}
			}
		}
		finally
		{
			IDisposable disposable;
			if ((disposable = (enumerator as IDisposable)) != null)
			{
				disposable.Dispose();
			}
		}
  -----------------------

Sandbox Fix
		
		
		//原理：Instance.CurrentSceneName里有所有的沙盒名字，通过存档Dump可以得知问题沙盒关卡为"Episode_6_Ice Sandbox"，其他类推。详见最下方完美存档Dump
		
		//同理，你也可以把SceneName换成其他的名字，来fine tune不同关卡的格子。
		BaseGameMode.InitGameMode
		if (object.Equals("Episode_6_Ice Sandbox", Singleton<GameManager>.Instance.CurrentSceneName))
		{
			List<int> currentConstructionGridRows = new List<int>
			{
				4095,
				4095,
				4095,
				4095,
				4095
			};
			base.CurrentConstructionGridRows = currentConstructionGridRows;
		}
-------------------
		
		
		LevelManager.CurrentConstructionGridRows
		if (object.Equals("Episode_6_Ice Sandbox", Singleton<GameManager>.Instance.CurrentSceneName))
			{
				return new List<int>
				{
					4095,
					4095,
					4095,
					4095,
					4095
				};
			}
-----------------------
		
		
		InGameCamera.Start
		if (object.Equals("Episode_6_Ice Sandbox", Singleton<GameManager>.Instance.CurrentSceneName))
		{
			this.m_cameraBuildZoom = 5.5f;
		}

----------------

完美存档dump
//方法：更改游戏Crypto算法的Encrypt，让其直接return clearTextByte。详见附件progress.dat		
强烈建议阅读https://www.h3xed.com/mobile/how-to-edit-bad-piggies-levels-building-grid-source-code 虽然文章中的方法已经不可用，但是此文章解释了上表中的intList和4095的来源。
