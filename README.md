# BadPiggiesEditLog
The Edit log of my BP Hack
-------------------
Grid & Camera Zoom hack
-----------------
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
-----------------
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




