# BadPiggiesEditLog
The Edit log of my BP Hack
-------------------
Grid & Camera Zoom hack


		BaseGameMode.InitGameMode
		using System.Collections.Generic;
		using System.Linq;
		using UnityEngine.SceneManagement;
		if (Singleton<GameManager>.Instance.CurrentEpisodeType == GameManager.EpisodeType.Sandbox && 				WPFMonoBehaviour.levelManager.CurrentGameMode is BaseGameMode)
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
		
		
		if (Singleton<GameManager>.Instance.CurrentEpisodeType == GameManager.EpisodeType.Sandbox && 					WPFMonoBehaviour.levelManager.CurrentGameMode is BaseGameMode)
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
		
		
		//原理：Instance.CurrentSceneName里有所有的沙盒名字，通过存档Dump可以得知问题沙盒关卡为"Episode_6_Ice Sandbox"，其他类推。详见		最下方完美存档Dump
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
//方法：更改游戏Crypto算法的Encrypt，让其直接return clearTextByte。
		
		
<data>
  <Boolean key="GameProgress_initialized" value="True" />
  <String key="InstallVersion" value="2.3.6" />
  <Int32 key="DataFormatVersion" value="6" />
  <String key="LastKnownVersion" value="2.3.6" />
  <Int32 key="player_level" value="131" />
  <Int32 key="player_experience" value="4196" />
  <Int32 key="player_pending_experience" value="-1" />
  <String key="Episode_1_Levels_cached_hash" value="6abad7f6472ffeb4550390d7379dd7ca" />
  <String key="Episode_2_Levels_cached_hash" value="9c3b54c180e6b9a585cab04b2f968d99" />
  <Int32 key="TimeOffset" value="-18000" />
  <String key="Episode_3_Levels_cached_hash" value="3d5e5a23395ba538a1e1365134ae3605" />
  <String key="DailyChallenge_0_LevelName" value="track_28" />
  <Int32 key="DailyChallenge_0_EpisodeIndex" value="3" />
  <Int32 key="DailyChallenge_0_LevelIndex" value="40" />
  <Int32 key="DailyChallenge_0_PositionIndex" value="0" />
  <Boolean key="DailyChallenge_0_Collected" value="True" />
  <Boolean key="DailyChallenge_0_Revealed" value="True" />
  <Boolean key="DailyChallenge_0_AdRevealed" value="True" />
  <String key="DailyChallenge_1_LevelName" value="test54" />
  <Int32 key="DailyChallenge_1_EpisodeIndex" value="2" />
  <Int32 key="DailyChallenge_1_LevelIndex" value="13" />
  <Int32 key="DailyChallenge_1_PositionIndex" value="0" />
  <Boolean key="DailyChallenge_1_Collected" value="True" />
  <Boolean key="DailyChallenge_1_Revealed" value="True" />
  <Boolean key="DailyChallenge_1_AdRevealed" value="True" />
  <String key="DailyChallenge_2_LevelName" value="scenario_39" />
  <Int32 key="DailyChallenge_2_EpisodeIndex" value="2" />
  <Int32 key="DailyChallenge_2_LevelIndex" value="32" />
  <Int32 key="DailyChallenge_2_PositionIndex" value="0" />
  <Boolean key="DailyChallenge_2_Collected" value="True" />
  <Boolean key="DailyChallenge_2_Revealed" value="True" />
  <Boolean key="DailyChallenge_2_AdRevealed" value="True" />
  <String key="TimerIds" value="daily_challenge_timer,LootCrateSlot_3" />
  <Int32 key="daily_challenge_timer_date" value="1578182400" />
  <String key="Episode_4_Levels_cached_hash" value="4906ed1e830cc88bc75394b18aeeae8b" />
  <String key="Episode_5_Levels_cached_hash" value="eccdab3be4ed0a065c29ca91388a3d49" />
  <String key="Episode_6_Levels_cached_hash" value="1870b96661ff860752cb97a6895818a0" />
  <String key="Episode_Race_Levels_cached_hash" value="828b01a465df0c13c3cee57d29bee242" />
  <String key="Episode_Sandbox_Levels_cached_hash" value="ca22faf751f9368fcd3567c5d39e535c" />
  <String key="Episode_Sandbox_Levels_2_cached_hash" value="fdf07fe5d44b347d5c968871d2294eb1" />
  <String key="Audio_Collection_cached_hash" value="ab7b306925837560888ab04d8c4ca4e7" />
  <String key="Music_Collection_cached_hash" value="d99e00accfecbd98d0da4bf829278584" />
  <Int32 key="button_unlock_SandboxLevelButton_S-1" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-2" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-7" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-8" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-3" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-4" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-5" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-6" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-S" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-9" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-10" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-D" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-M" value="1" />
  <Int32 key="button_unlock_SandboxLevelButton_S-F" value="1" />
  <Int32 key="Episode1_Start_played" value="1" />
  <Int32 key="TutorialBookLastOpenedPage" value="144" />
  <Int32 key="TutorialBookFirstOpenedPage" value="0" />
  <String key="MenuBackground" value="Background_Night_01_SET 1" />
  <Int32 key="StartedLevel Level_21" value="1" />
  <Int32 key="Level_21_contraption" value="1" />
  <Int32 key="Level_21_challenge_0" value="2" />
  <Int32 key="Level_21_challenge_1" value="2" />
  <Int32 key="Level_21_challenge_2" value="2" />
  <Int32 key="SnoutCoins" value="99999" />
  <Int32 key="exp_LevelComplete1StarLevel_21" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_21" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_21" value="1" />
  <Int32 key="Level_21_stars" value="3" />
  <Boolean key="FlurryEventSent_All Basic Content Played" value="True" />
  <Int32 key="tried_to_ask_notifications_counter" value="140" />
  <Boolean key="are_notifications_allowed" value="True" />
  <Int32 key="FreeShopCrateWood" value="1" />
  <Boolean key="AnyLootCrateCollected" value="True" />
  <Int32 key="Scrap" value="26697" />
  <Boolean key="Pre_FirstRewardGiven" value="True" />
  <Boolean key="Part_Pig_02_SET" value="True" />
  <Boolean key="Part_Pig_02_SET_isNew" value="False" />
  <Int32 key="NewParts" value="0" />
  <Boolean key="Part_Pig_02_SET_isUsed" value="True" />
  <Int32 key="Crate_amount_Wood" value="0" />
  <Int32 key="Wood_crates_collected" value="26" />
  <Int32 key="Total_parts_scrapped" value="228" />
  <Int32 key="Total_parts_received" value="229" />
  <Int32 key="Level_Sandbox_04_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_04" value="1" />
  <Int32 key="Level_Sandbox_04_contraption" value="1" />
  <Int32 key="Level_Sandbox_04_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_04_stars" value="20" />
  <Int32 key="TutorialBookOpenCount" value="5" />
  <Boolean key="PowerupTutorialShown" value="True" />
  <Int32 key="SuperGlue_Available" value="100001" />
  <Int32 key="Level_Sandbox_04_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox16" value="2" />
  <Int32 key="TurboCharge_Available" value="99998" />
  <Int32 key="SuperMagnet_Available" value="99998" />
  <Int32 key="Level_Sandbox_04_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_02_LastLoadedContraptionSlotIndex" value="0" />
  <Boolean key="Workshop_Visited" value="True" />
  <Int32 key="Workshop_Tutorial" value="3" />
  <Int32 key="Machine_scrap_amount" value="0" />
  <Int32 key="Pre_RewardsGiven" value="10" />
  <Boolean key="Pre_RewardGiven_EngineSmall" value="True" />
  <Boolean key="Part_EngineSmall_07_SET" value="True" />
  <Boolean key="Part_EngineSmall_07_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_07_SET_isUsed" value="True" />
  <Int32 key="CraftCountCommon" value="71" />
  <Boolean key="Pre_RewardGiven_WoodenFrame" value="True" />
  <Boolean key="Part_WoodenFrame_02_SET" value="True" />
  <Boolean key="Part_WoodenFrame_02_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_02_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_CartWheel" value="True" />
  <Boolean key="Part_CartWheel_04_SET" value="True" />
  <Boolean key="Part_CartWheel_04_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_04_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_EngineBig" value="True" />
  <Boolean key="Part_EngineBig_02_SET" value="True" />
  <Boolean key="Part_EngineBig_02_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_02_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_StickyWheel" value="True" />
  <Boolean key="Part_StickyWheel_04_SET" value="True" />
  <Boolean key="Part_StickyWheel_04_SET_isNew" value="False" />
  <Boolean key="Part_StickyWheel_04_SET_isUsed" value="True" />
  <Int32 key="CraftCountEpic" value="73" />
  <Boolean key="Pre_RewardGiven_MotorWheel" value="True" />
  <Boolean key="Part_MotorWheel_05_SET" value="True" />
  <Boolean key="Part_MotorWheel_05_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_05_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_MetalFrame" value="True" />
  <Boolean key="Part_MetalFrame_07_SET" value="True" />
  <Boolean key="Part_MetalFrame_07_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_07_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_Egg" value="True" />
  <Boolean key="Part_Egg_04_SET" value="True" />
  <Boolean key="Part_Egg_04_SET_isNew" value="False" />
  <Boolean key="Part_Egg_04_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_Engine" value="True" />
  <Boolean key="Part_Engine_04_SET" value="True" />
  <Boolean key="Part_Engine_04_SET_isNew" value="False" />
  <Boolean key="Part_Engine_04_SET_isUsed" value="True" />
  <Boolean key="Pre_RewardGiven_Balloon" value="True" />
  <Boolean key="Part_Balloon_08_SET" value="True" />
  <Boolean key="Part_Balloon_08_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_08_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_08_SET" value="True" />
  <Boolean key="Part_Balloons3_08_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_08_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_07_SET" value="True" />
  <Boolean key="Part_CartWheel_07_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_07_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenWings_04_SET" value="True" />
  <Boolean key="Part_WoodenWings_04_SET_isNew" value="False" />
  <Boolean key="Part_WoodenWings_04_SET_isUsed" value="True" />
  <Boolean key="Part_Rope_04_SET" value="True" />
  <Boolean key="Part_Rope_04_SET_isNew" value="False" />
  <Boolean key="Part_Rope_04_SET_isUsed" value="True" />
  <Boolean key="Part_SpringBoxingGlove_04_SET" value="True" />
  <Boolean key="Part_SpringBoxingGlove_04_SET_isNew" value="False" />
  <Boolean key="Part_SpringBoxingGlove_04_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_10_SET" value="True" />
  <Boolean key="Part_MetalFrame_10_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_10_SET_isUsed" value="True" />
  <Boolean key="Part_PoweredUmbrella_04_SET" value="True" />
  <Boolean key="Part_PoweredUmbrella_04_SET_isNew" value="False" />
  <Boolean key="Part_PoweredUmbrella_04_SET_isUsed" value="True" />
  <Boolean key="Part_SpotLight_04_SET" value="True" />
  <Boolean key="Part_SpotLight_04_SET_isNew" value="False" />
  <Boolean key="Part_SpotLight_04_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenTail_04_SET" value="True" />
  <Boolean key="Part_WoodenTail_04_SET_isNew" value="False" />
  <Boolean key="Part_WoodenTail_04_SET_isUsed" value="True" />
  <Boolean key="Part_Rocket_04_SET" value="True" />
  <Boolean key="Part_Rocket_04_SET_isNew" value="False" />
  <Boolean key="Part_Rocket_04_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_10_SET" value="True" />
  <Boolean key="Part_CartWheel_10_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_10_SET_isUsed" value="True" />
  <Boolean key="Part_RedRocket_04_SET" value="True" />
  <Boolean key="Part_RedRocket_04_SET_isNew" value="False" />
  <Boolean key="Part_RedRocket_04_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags2_04_SET" value="True" />
  <Boolean key="Part_Sandbags2_04_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags2_04_SET_isUsed" value="True" />
  <Boolean key="Part_Kicker_4" value="True" />
  <Boolean key="Part_Kicker_4_isNew" value="False" />
  <Boolean key="Part_Kicker_4_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_07_SET" value="True" />
  <Boolean key="Part_MotorWheel_07_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_07_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_04_SET" value="True" />
  <Boolean key="Part_Umbrella_04_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_04_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_06_SET" value="True" />
  <Boolean key="Part_CartWheel_06_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_06_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_04_SET" value="True" />
  <Boolean key="Part_EngineBig_04_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_04_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_07_SET" value="True" />
  <Boolean key="Part_Rotor_07_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_07_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_06_SET" value="True" />
  <Boolean key="Part_EngineBig_06_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_06_SET_isUsed" value="True" />
  <Boolean key="Part_GrapplingHook_05_SET" value="True" />
  <Boolean key="Part_GrapplingHook_05_SET_isNew" value="False" />
  <Boolean key="Part_GrapplingHook_05_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags3_04_SET" value="True" />
  <Boolean key="Part_Sandbags3_04_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags3_04_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_05_SET" value="True" />
  <Boolean key="Part_WoodenFrame_05_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_05_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_06_SET" value="True" />
  <Boolean key="Part_Umbrella_06_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_06_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_05_SET" value="True" />
  <Boolean key="Part_NormalWheel_05_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_05_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_07_SET" value="True" />
  <Boolean key="Part_NormalWheel_07_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_07_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_06_SET" value="True" />
  <Boolean key="Part_KingPig_06_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_06_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_07_SET" value="True" />
  <Boolean key="Part_Balloons2_07_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_07_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenWings_05_SET" value="True" />
  <Boolean key="Part_WoodenWings_05_SET_isNew" value="False" />
  <Boolean key="Part_WoodenWings_05_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_10_SET" value="True" />
  <Boolean key="Part_Pig_10_SET_isNew" value="False" />
  <Boolean key="Part_Pig_10_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_07_SET" value="True" />
  <Boolean key="Part_PlanePropeller_07_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_07_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_04_SET" value="True" />
  <Boolean key="Part_Rotor_04_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_04_SET_isUsed" value="True" />
  <Boolean key="Part_MetalWings_04_SET" value="True" />
  <Boolean key="Part_MetalWings_04_SET_isNew" value="False" />
  <Boolean key="Part_MetalWings_04_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_07_SET" value="True" />
  <Boolean key="Part_Balloon_07_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_07_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_05_SET" value="True" />
  <Boolean key="Part_TNT_05_SET_isNew" value="False" />
  <Boolean key="Part_TNT_05_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_05_SET" value="True" />
  <Boolean key="Part_Gearbox_05_SET_isNew" value="False" />
  <Boolean key="Part_Gearbox_05_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_09_SET" value="True" />
  <Boolean key="Part_EngineSmall_09_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_09_SET_isUsed" value="True" />
  <Boolean key="Part_Engine_06_SET" value="True" />
  <Boolean key="Part_Engine_06_SET_isNew" value="False" />
  <Boolean key="Part_Engine_06_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_08_SET" value="True" />
  <Boolean key="Part_Balloons2_08_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_08_SET_isUsed" value="True" />
  <Boolean key="Part_CokeBottle_04_SET" value="True" />
  <Boolean key="Part_CokeBottle_04_SET_isNew" value="False" />
  <Boolean key="Part_CokeBottle_04_SET_isUsed" value="True" />
  <Boolean key="Part_GoldenPig_04_SET" value="True" />
  <Boolean key="Part_GoldenPig_04_SET_isNew" value="False" />
  <Boolean key="Part_GoldenPig_04_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_04_SET" value="True" />
  <Boolean key="Part_TNT_04_SET_isNew" value="False" />
  <Boolean key="Part_TNT_04_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_15_SET 5" value="True" />
  <Boolean key="Part_Pig_15_SET 5_isNew" value="False" />
  <Boolean key="Part_Pig_15_SET 5_isUsed" value="True" />
  <Boolean key="Part_MetalTail_04_SET" value="True" />
  <Boolean key="Part_MetalTail_04_SET_isNew" value="False" />
  <Boolean key="Part_MetalTail_04_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_05_SET" value="True" />
  <Boolean key="Part_Balloons2_05_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_05_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_05_SET" value="True" />
  <Boolean key="Part_MetalFrame_05_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_05_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_09_SET" value="True" />
  <Boolean key="Part_WoodenFrame_09_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_09_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_07_SET" value="True" />
  <Boolean key="Part_SmallWheel_07_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_07_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_17_SET" value="True" />
  <Boolean key="Part_Pig_17_SET_isNew" value="False" />
  <Boolean key="Part_Pig_17_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_04_SET" value="True" />
  <Boolean key="Part_Fan_04_SET_isNew" value="False" />
  <Boolean key="Part_Fan_04_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_09_SET" value="True" />
  <Boolean key="Part_Pig_09_SET_isNew" value="False" />
  <Boolean key="Part_Pig_09_SET_isUsed" value="True" />
  <Boolean key="Part_PointLight_04_SET" value="True" />
  <Boolean key="Part_PointLight_04_SET_isNew" value="False" />
  <Boolean key="Part_PointLight_04_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_04_SET" value="True" />
  <Boolean key="Part_PlanePropeller_04_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_04_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_05_SET" value="True" />
  <Boolean key="Part_SmallWheel_05_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_05_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_05_SET" value="True" />
  <Boolean key="Part_Balloons3_05_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_05_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_07_SET" value="True" />
  <Boolean key="Part_Balloons3_07_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_07_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_05_SET" value="True" />
  <Boolean key="Part_Bellows_05_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_05_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_05_SET" value="True" />
  <Boolean key="Part_Balloon_05_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_05_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_08_SET" value="True" />
  <Boolean key="Part_Pig_08_SET_isNew" value="False" />
  <Boolean key="Part_Pig_08_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_04_SET" value="True" />
  <Boolean key="Part_KingPig_04_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_04_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_06_SET" value="True" />
  <Boolean key="Part_WoodenFrame_06_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_06_SET_isUsed" value="True" />
  <Boolean key="Part_SodaBottle_04_SET" value="True" />
  <Boolean key="Part_SodaBottle_04_SET_isNew" value="False" />
  <Boolean key="Part_SodaBottle_04_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_05_SET" value="True" />
  <Boolean key="Part_Sandbag_05_SET_isNew" value="False" />
  <Boolean key="Part_Sandbag_05_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_06_SET" value="True" />
  <Boolean key="Part_Bellows_06_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_06_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_04_SET" value="True" />
  <Boolean key="Part_Sandbag_04_SET_isNew" value="False" />
  <Boolean key="Part_Sandbag_04_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_04_SET" value="True" />
  <Boolean key="Part_EngineSmall_04_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_04_SET_isUsed" value="True" />
  <Boolean key="Part_Spring_04_SET" value="True" />
  <Boolean key="Part_Spring_04_SET_isNew" value="False" />
  <Boolean key="Part_Spring_04_SET_isUsed" value="True" />
  <Boolean key="Part_Spring_03_SET" value="True" />
  <Boolean key="Part_Spring_03_SET_isNew" value="False" />
  <Boolean key="Part_Spring_03_SET_isUsed" value="True" />
  <Int32 key="CraftCountRare" value="78" />
  <Boolean key="Part_GoldenPig_03_SET" value="True" />
  <Boolean key="Part_GoldenPig_03_SET_isNew" value="False" />
  <Boolean key="Part_GoldenPig_03_SET_isUsed" value="True" />
  <Boolean key="Part_Engine_05_SET" value="True" />
  <Boolean key="Part_Engine_05_SET_isNew" value="False" />
  <Boolean key="Part_Engine_05_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_03_SET" value="True" />
  <Boolean key="Part_Umbrella_03_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_03_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_05_SET" value="True" />
  <Boolean key="Part_CartWheel_05_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_05_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_05_SET" value="True" />
  <Boolean key="Part_Pig_05_SET_isNew" value="False" />
  <Boolean key="Part_Pig_05_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_03_SET" value="True" />
  <Boolean key="Part_Fan_03_SET_isNew" value="False" />
  <Boolean key="Part_Fan_03_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_03_SET" value="True" />
  <Boolean key="Part_EngineBig_03_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_03_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_06_SET" value="True" />
  <Boolean key="Part_EngineSmall_06_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_06_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_03_SET" value="True" />
  <Boolean key="Part_PlanePropeller_03_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_03_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_03_SET" value="True" />
  <Boolean key="Part_EngineSmall_03_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_03_SET_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_04_SET" value="True" />
  <Boolean key="Part_MotorWheel_04_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_04_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_06_SET" value="True" />
  <Boolean key="Part_Balloons3_06_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_06_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_04_SET" value="True" />
  <Boolean key="Part_SmallWheel_04_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_04_SET_isUsed" value="True" />
  <Boolean key="Part_MetalTail_03_SET" value="True" />
  <Boolean key="Part_MetalTail_03_SET_isNew" value="False" />
  <Boolean key="Part_MetalTail_03_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_14_SET 4" value="True" />
  <Boolean key="Part_Pig_14_SET 4_isNew" value="False" />
  <Boolean key="Part_Pig_14_SET 4_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_08_SET" value="True" />
  <Boolean key="Part_WoodenFrame_08_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_08_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_08_SET" value="True" />
  <Boolean key="Part_PlanePropeller_08_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_08_SET_isUsed" value="True" />
  <Boolean key="Part_CokeBottle_03_SET" value="True" />
  <Boolean key="Part_CokeBottle_03_SET_isNew" value="False" />
  <Boolean key="Part_CokeBottle_03_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_04_SET" value="True" />
  <Boolean key="Part_NormalWheel_04_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_04_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_11_SET" value="True" />
  <Boolean key="Part_CartWheel_11_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_11_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenTail_03_SET" value="True" />
  <Boolean key="Part_WoodenTail_03_SET_isNew" value="False" />
  <Boolean key="Part_WoodenTail_03_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_03_SET" value="True" />
  <Boolean key="Part_Rotor_03_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_03_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_05_SET" value="True" />
  <Boolean key="Part_Umbrella_05_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_05_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_04_SET" value="True" />
  <Boolean key="Part_Gearbox_04_SET_isNew" value="False" />
  <Boolean key="Part_Gearbox_04_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_08_SET" value="True" />
  <Boolean key="Part_Rotor_08_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_08_SET_isUsed" value="True" />
  <Boolean key="Part_Rope_03_SET" value="True" />
  <Boolean key="Part_Rope_03_SET_isNew" value="False" />
  <Boolean key="Part_Rope_03_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_08_SET" value="True" />
  <Boolean key="Part_CartWheel_08_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_08_SET_isUsed" value="True" />
  <Boolean key="Part_StickyWheel_03_SET" value="True" />
  <Boolean key="Part_StickyWheel_03_SET_isNew" value="False" />
  <Boolean key="Part_StickyWheel_03_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_06_SET" value="True" />
  <Boolean key="Part_Sandbag_06_SET_isNew" value="False" />
  <Boolean key="Part_Sandbag_06_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_09_SET" value="True" />
  <Boolean key="Part_MetalFrame_09_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_09_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_16_SET" value="True" />
  <Boolean key="Part_Pig_16_SET_isNew" value="False" />
  <Boolean key="Part_Pig_16_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_04_SET" value="True" />
  <Boolean key="Part_Bellows_04_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_04_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_09_SET" value="True" />
  <Boolean key="Part_CartWheel_09_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_09_SET_isUsed" value="True" />
  <Boolean key="Part_PoweredUmbrella_03_SET" value="True" />
  <Boolean key="Part_PoweredUmbrella_03_SET_isNew" value="False" />
  <Boolean key="Part_PoweredUmbrella_03_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_06_SET" value="True" />
  <Boolean key="Part_PlanePropeller_06_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_06_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_13_SET 3" value="True" />
  <Boolean key="Part_Pig_13_SET 3_isNew" value="False" />
  <Boolean key="Part_Pig_13_SET 3_isUsed" value="True" />
  <Boolean key="Part_Balloons2_04_SET" value="True" />
  <Boolean key="Part_Balloons2_04_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_04_SET_isUsed" value="True" />
  <Boolean key="Part_SpringBoxingGlove_03_SET" value="True" />
  <Boolean key="Part_SpringBoxingGlove_03_SET_isNew" value="False" />
  <Boolean key="Part_SpringBoxingGlove_03_SET_isUsed" value="True" />
  <Boolean key="Part_SodaBottle_03_SET" value="True" />
  <Boolean key="Part_SodaBottle_03_SET_isNew" value="False" />
  <Boolean key="Part_SodaBottle_03_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_08_SET" value="True" />
  <Boolean key="Part_Bellows_08_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_08_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_05_SET" value="True" />
  <Boolean key="Part_EngineBig_05_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_05_SET_isUsed" value="True" />
  <Boolean key="Part_PointLight_03_SET" value="True" />
  <Boolean key="Part_PointLight_03_SET_isNew" value="False" />
  <Boolean key="Part_PointLight_03_SET_isUsed" value="True" />
  <Boolean key="Part_Kicker_5" value="True" />
  <Boolean key="Part_Kicker_5_isNew" value="False" />
  <Boolean key="Part_Kicker_5_isUsed" value="True" />
  <Boolean key="Part_Engine_03_SET" value="True" />
  <Boolean key="Part_Engine_03_SET_isNew" value="False" />
  <Boolean key="Part_Engine_03_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_03_SET" value="True" />
  <Boolean key="Part_KingPig_03_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_03_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_04_SET" value="True" />
  <Boolean key="Part_Balloons3_04_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_04_SET_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_03_SET" value="True" />
  <Boolean key="Part_MotorWheel_03_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_03_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_06_SET" value="True" />
  <Boolean key="Part_SmallWheel_06_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_06_SET_isUsed" value="True" />
  <Boolean key="Part_GrapplingHook_03_SET" value="True" />
  <Boolean key="Part_GrapplingHook_03_SET_isNew" value="False" />
  <Boolean key="Part_GrapplingHook_03_SET_isUsed" value="True" />
  <Boolean key="Part_Kicker_3" value="True" />
  <Boolean key="Part_Kicker_3_isNew" value="False" />
  <Boolean key="Part_Kicker_3_isUsed" value="True" />
  <Boolean key="Part_Pig_07_SET" value="True" />
  <Boolean key="Part_Pig_07_SET_isNew" value="False" />
  <Boolean key="Part_Pig_07_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_06_SET" value="True" />
  <Boolean key="Part_Gearbox_06_SET_isNew" value="False" />
  <Boolean key="Part_Gearbox_06_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_08_SET" value="True" />
  <Boolean key="Part_EngineSmall_08_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_08_SET_isUsed" value="True" />
  <Boolean key="Part_Rocket_03_SET" value="True" />
  <Boolean key="Part_Rocket_03_SET_isNew" value="False" />
  <Boolean key="Part_Rocket_03_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_04_SET" value="True" />
  <Boolean key="Part_Balloon_04_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_04_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_03_SET" value="True" />
  <Boolean key="Part_MetalFrame_03_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_03_SET_isUsed" value="True" />
  <Boolean key="Part_Egg_03_SET" value="True" />
  <Boolean key="Part_Egg_03_SET_isNew" value="False" />
  <Boolean key="Part_Egg_03_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_04_SET" value="True" />
  <Boolean key="Part_MetalFrame_04_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_04_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags2_03_SET" value="True" />
  <Boolean key="Part_Sandbags2_03_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags2_03_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_06_SET" value="True" />
  <Boolean key="Part_Balloons2_06_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_06_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_03_SET" value="True" />
  <Boolean key="Part_NormalWheel_03_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_03_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_06_SET" value="True" />
  <Boolean key="Part_Pig_06_SET_isNew" value="False" />
  <Boolean key="Part_Pig_06_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_05_SET" value="True" />
  <Boolean key="Part_Fan_05_SET_isNew" value="False" />
  <Boolean key="Part_Fan_05_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_06_SET" value="True" />
  <Boolean key="Part_Balloon_06_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_06_SET_isUsed" value="True" />
  <Boolean key="Part_RedRocket_03_SET" value="True" />
  <Boolean key="Part_RedRocket_03_SET_isNew" value="False" />
  <Boolean key="Part_RedRocket_03_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags3_03_SET" value="True" />
  <Boolean key="Part_Sandbags3_03_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags3_03_SET_isUsed" value="True" />
  <Boolean key="Part_GrapplingHook_04_SET" value="True" />
  <Boolean key="Part_GrapplingHook_04_SET_isNew" value="False" />
  <Boolean key="Part_GrapplingHook_04_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_03_SET" value="True" />
  <Boolean key="Part_Sandbag_03_SET_isNew" value="False" />
  <Boolean key="Part_Sandbag_03_SET_isUsed" value="True" />
  <Boolean key="Part_MetalWings_03_SET" value="True" />
  <Boolean key="Part_MetalWings_03_SET_isNew" value="False" />
  <Boolean key="Part_MetalWings_03_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_11_SET" value="True" />
  <Boolean key="Part_MetalFrame_11_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_11_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenWings_03_SET" value="True" />
  <Boolean key="Part_WoodenWings_03_SET_isNew" value="False" />
  <Boolean key="Part_WoodenWings_03_SET_isUsed" value="True" />
  <Boolean key="Part_SpotLight_03_SET" value="True" />
  <Boolean key="Part_SpotLight_03_SET_isNew" value="False" />
  <Boolean key="Part_SpotLight_03_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_03_SET" value="True" />
  <Boolean key="Part_TNT_03_SET_isNew" value="False" />
  <Boolean key="Part_TNT_03_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_07_SET" value="True" />
  <Boolean key="Part_WoodenFrame_07_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_07_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_05_SET" value="True" />
  <Boolean key="Part_KingPig_05_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_05_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_04_SET" value="True" />
  <Boolean key="Part_WoodenFrame_04_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_04_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_06_SET" value="True" />
  <Boolean key="Part_Rotor_06_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_06_SET_isUsed" value="True" />
  <Boolean key="Part_Rope_02_SET" value="True" />
  <Boolean key="Part_Rope_02_SET_isNew" value="False" />
  <Boolean key="Part_Rope_02_SET_isUsed" value="True" />
  <Boolean key="Part_PoweredUmbrella_02_SET" value="True" />
  <Boolean key="Part_PoweredUmbrella_02_SET_isNew" value="False" />
  <Boolean key="Part_PoweredUmbrella_02_SET_isUsed" value="True" />
  <Boolean key="Part_Egg_02_SET" value="True" />
  <Boolean key="Part_Egg_02_SET_isNew" value="False" />
  <Boolean key="Part_Egg_02_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_02_SET" value="True" />
  <Boolean key="Part_Balloon_02_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_02_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_02_SET" value="True" />
  <Boolean key="Part_Umbrella_02_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_02_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_19_SET" value="True" />
  <Boolean key="Part_Pig_19_SET_isNew" value="False" />
  <Boolean key="Part_Pig_19_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags3_02_SET" value="True" />
  <Boolean key="Part_Sandbags3_02_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags3_02_SET_isUsed" value="True" />
  <Boolean key="Part_Rocket_02_SET" value="True" />
  <Boolean key="Part_Rocket_02_SET_isNew" value="False" />
  <Boolean key="Part_Rocket_02_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_08_SET" value="True" />
  <Boolean key="Part_MetalFrame_08_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_08_SET_isUsed" value="True" />
  <Boolean key="Part_GrapplingHook_02_SET" value="True" />
  <Boolean key="Part_GrapplingHook_02_SET_isNew" value="False" />
  <Boolean key="Part_GrapplingHook_02_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_06_SET" value="True" />
  <Boolean key="Part_MetalFrame_06_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_06_SET_isUsed" value="True" />
  <Boolean key="Part_Kicker_2" value="True" />
  <Boolean key="Part_Kicker_2_isNew" value="False" />
  <Boolean key="Part_Kicker_2_isUsed" value="True" />
  <Boolean key="Part_Balloons3_02_SET" value="True" />
  <Boolean key="Part_Balloons3_02_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_02_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_02_SET" value="True" />
  <Boolean key="Part_Bellows_02_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_02_SET_isUsed" value="True" />
  <Boolean key="Part_Engine_07_SET" value="True" />
  <Boolean key="Part_Engine_07_SET_isNew" value="False" />
  <Boolean key="Part_Engine_07_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_02_SET" value="True" />
  <Boolean key="Part_KingPig_02_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_02_SET_isUsed" value="True" />
  <Boolean key="Part_RedRocket_02_SET" value="True" />
  <Boolean key="Part_RedRocket_02_SET_isNew" value="False" />
  <Boolean key="Part_RedRocket_02_SET_isUsed" value="True" />
  <Boolean key="Part_CokeBottle_02_SET" value="True" />
  <Boolean key="Part_CokeBottle_02_SET_isNew" value="False" />
  <Boolean key="Part_CokeBottle_02_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_04_SET" value="True" />
  <Boolean key="Part_Pig_04_SET_isNew" value="False" />
  <Boolean key="Part_Pig_04_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_03_SET" value="True" />
  <Boolean key="Part_Balloons2_03_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_03_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_02_SET" value="True" />
  <Boolean key="Part_Balloons2_02_SET_isNew" value="False" />
  <Boolean key="Part_Balloons2_02_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_03_SET" value="True" />
  <Boolean key="Part_Pig_03_SET_isNew" value="False" />
  <Boolean key="Part_Pig_03_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_03_SET" value="True" />
  <Boolean key="Part_Gearbox_03_SET_isNew" value="False" />
  <Boolean key="Part_Gearbox_03_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_06_SET" value="True" />
  <Boolean key="Part_NormalWheel_06_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_06_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_03_SET" value="True" />
  <Boolean key="Part_Balloons3_03_SET_isNew" value="False" />
  <Boolean key="Part_Balloons3_03_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_05_SET" value="True" />
  <Boolean key="Part_Rotor_05_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_05_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_03_SET" value="True" />
  <Boolean key="Part_CartWheel_03_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_03_SET_isUsed" value="True" />
  <Boolean key="Part_PointLight_02_SET" value="True" />
  <Boolean key="Part_PointLight_02_SET_isNew" value="False" />
  <Boolean key="Part_PointLight_02_SET_isUsed" value="True" />
  <Boolean key="Part_GoldenPig_02_SET" value="True" />
  <Boolean key="Part_GoldenPig_02_SET_isNew" value="False" />
  <Boolean key="Part_GoldenPig_02_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_02_SET" value="True" />
  <Boolean key="Part_Sandbag_02_SET_isNew" value="False" />
  <Boolean key="Part_Sandbag_02_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_02_SET" value="True" />
  <Boolean key="Part_NormalWheel_02_SET_isNew" value="False" />
  <Boolean key="Part_NormalWheel_02_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_09_SET" value="True" />
  <Boolean key="Part_PlanePropeller_09_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_09_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_05_SET" value="True" />
  <Boolean key="Part_PlanePropeller_05_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_05_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_02_SET" value="True" />
  <Boolean key="Part_Rotor_02_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_02_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_12_SET 2" value="True" />
  <Boolean key="Part_Pig_12_SET 2_isNew" value="False" />
  <Boolean key="Part_Pig_12_SET 2_isUsed" value="True" />
  <Boolean key="Part_WoodenTail_02_SET" value="True" />
  <Boolean key="Part_WoodenTail_02_SET_isNew" value="False" />
  <Boolean key="Part_WoodenTail_02_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_02_SET" value="True" />
  <Boolean key="Part_Gearbox_02_SET_isNew" value="False" />
  <Boolean key="Part_Gearbox_02_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_03_SET" value="True" />
  <Boolean key="Part_Balloon_03_SET_isNew" value="False" />
  <Boolean key="Part_Balloon_03_SET_isUsed" value="True" />
  <Boolean key="Part_SodaBottle_02_SET" value="True" />
  <Boolean key="Part_SodaBottle_02_SET_isNew" value="False" />
  <Boolean key="Part_SodaBottle_02_SET_isUsed" value="True" />
  <Boolean key="Part_SpringBoxingGlove_02_SET" value="True" />
  <Boolean key="Part_SpringBoxingGlove_02_SET_isNew" value="False" />
  <Boolean key="Part_SpringBoxingGlove_02_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_02_SET" value="True" />
  <Boolean key="Part_SmallWheel_02_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_02_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_02_SET" value="True" />
  <Boolean key="Part_MetalFrame_02_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_02_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenWings_02_SET" value="True" />
  <Boolean key="Part_WoodenWings_02_SET_isNew" value="False" />
  <Boolean key="Part_WoodenWings_02_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_10_SET" value="True" />
  <Boolean key="Part_Rotor_10_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_10_SET_isUsed" value="True" />
  <Boolean key="Part_MetalTail_02_SET" value="True" />
  <Boolean key="Part_MetalTail_02_SET_isNew" value="False" />
  <Boolean key="Part_MetalTail_02_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_10_SET" value="True" />
  <Boolean key="Part_EngineSmall_10_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_10_SET_isUsed" value="True" />
  <Boolean key="Part_Spring_02_SET" value="True" />
  <Boolean key="Part_Spring_02_SET_isNew" value="False" />
  <Boolean key="Part_Spring_02_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_02_SET" value="True" />
  <Boolean key="Part_CartWheel_02_SET_isNew" value="False" />
  <Boolean key="Part_CartWheel_02_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_02_SET" value="True" />
  <Boolean key="Part_TNT_02_SET_isNew" value="False" />
  <Boolean key="Part_TNT_02_SET_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_02_SET" value="True" />
  <Boolean key="Part_MotorWheel_02_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_02_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_10_SET" value="True" />
  <Boolean key="Part_WoodenFrame_10_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_10_SET_isUsed" value="True" />
  <Boolean key="Part_StickyWheel_02_SET" value="True" />
  <Boolean key="Part_StickyWheel_02_SET_isNew" value="False" />
  <Boolean key="Part_StickyWheel_02_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_03_SET" value="True" />
  <Boolean key="Part_SmallWheel_03_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_03_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_11_SET 1" value="True" />
  <Boolean key="Part_Pig_11_SET 1_isNew" value="False" />
  <Boolean key="Part_Pig_11_SET 1_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_02_SET" value="True" />
  <Boolean key="Part_EngineSmall_02_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_02_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_07_SET" value="True" />
  <Boolean key="Part_EngineBig_07_SET_isNew" value="False" />
  <Boolean key="Part_EngineBig_07_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_03_SET" value="True" />
  <Boolean key="Part_WoodenFrame_03_SET_isNew" value="False" />
  <Boolean key="Part_WoodenFrame_03_SET_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_06_SET" value="True" />
  <Boolean key="Part_MotorWheel_06_SET_isNew" value="False" />
  <Boolean key="Part_MotorWheel_06_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_02_SET" value="True" />
  <Boolean key="Part_PlanePropeller_02_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_02_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_02_SET" value="True" />
  <Boolean key="Part_Fan_02_SET_isNew" value="False" />
  <Boolean key="Part_Fan_02_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_03_SET" value="True" />
  <Boolean key="Part_Bellows_03_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_03_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags2_02_SET" value="True" />
  <Boolean key="Part_Sandbags2_02_SET_isNew" value="False" />
  <Boolean key="Part_Sandbags2_02_SET_isUsed" value="True" />
  <Boolean key="Part_MetalWings_02_SET" value="True" />
  <Boolean key="Part_MetalWings_02_SET_isNew" value="False" />
  <Boolean key="Part_MetalWings_02_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_07_SET" value="True" />
  <Boolean key="Part_Umbrella_07_SET_isNew" value="False" />
  <Boolean key="Part_Umbrella_07_SET_isUsed" value="True" />
  <Boolean key="Part_Engine_02_SET" value="True" />
  <Boolean key="Part_Engine_02_SET_isNew" value="False" />
  <Boolean key="Part_Engine_02_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_07_SET" value="True" />
  <Boolean key="Part_KingPig_07_SET_isNew" value="False" />
  <Boolean key="Part_KingPig_07_SET_isUsed" value="True" />
  <Boolean key="Part_SpotLight_02_SET" value="True" />
  <Boolean key="Part_SpotLight_02_SET_isNew" value="False" />
  <Boolean key="Part_SpotLight_02_SET_isUsed" value="True" />
  <Boolean key="AlienCraftingMachineShown" value="True" />
  <Boolean key="Part_EngineSmall_05_SET" value="True" />
  <Boolean key="Part_EngineSmall_05_SET_isNew" value="False" />
  <Boolean key="Part_EngineSmall_05_SET_isUsed" value="True" />
  <Int32 key="CraftCountLegendary" value="15" />
  <Boolean key="Part_GrapplingHook_06_SET" value="True" />
  <Boolean key="Part_GrapplingHook_06_SET_isNew" value="False" />
  <Boolean key="Part_GrapplingHook_06_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_07_SET" value="True" />
  <Boolean key="Part_Bellows_07_SET_isNew" value="False" />
  <Boolean key="Part_Bellows_07_SET_isUsed" value="True" />
  <Boolean key="Part_SpringBoxingGlove_05_SET" value="True" />
  <Boolean key="Part_SpringBoxingGlove_05_SET_isNew" value="False" />
  <Boolean key="Part_SpringBoxingGlove_05_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_06_SET" value="True" />
  <Boolean key="Part_TNT_06_SET_isNew" value="False" />
  <Boolean key="Part_TNT_06_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_01_SET_isUsed" value="True" />
  <Boolean key="Part_KingPig_01_SET_isUsed" value="True" />
  <Boolean key="Part_PointLight_05_SET" value="True" />
  <Boolean key="Part_PointLight_05_SET_isNew" value="False" />
  <Boolean key="Part_PointLight_05_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_06_SET" value="True" />
  <Boolean key="Part_Fan_06_SET_isNew" value="False" />
  <Boolean key="Part_Fan_06_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_12_SET" value="True" />
  <Boolean key="Part_MetalFrame_12_SET_isNew" value="False" />
  <Boolean key="Part_MetalFrame_12_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_10_SET" value="True" />
  <Boolean key="Part_PlanePropeller_10_SET_isNew" value="False" />
  <Boolean key="Part_PlanePropeller_10_SET_isUsed" value="True" />
  <Boolean key="Part_SodaBottle_05_SET" value="True" />
  <Boolean key="Part_SodaBottle_05_SET_isNew" value="False" />
  <Boolean key="Part_SodaBottle_05_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_08_SET" value="True" />
  <Boolean key="Part_SmallWheel_08_SET_isNew" value="False" />
  <Boolean key="Part_SmallWheel_08_SET_isUsed" value="True" />
  <Boolean key="Part_CokeBottle_05_SET" value="True" />
  <Boolean key="Part_CokeBottle_05_SET_isNew" value="False" />
  <Boolean key="Part_CokeBottle_05_SET_isUsed" value="True" />
  <Boolean key="Part_Egg_06_SET" value="True" />
  <Boolean key="Part_Egg_06_SET_isNew" value="False" />
  <Boolean key="Part_Egg_06_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_09_SET" value="True" />
  <Boolean key="Part_Rotor_09_SET_isNew" value="False" />
  <Boolean key="Part_Rotor_09_SET_isUsed" value="True" />
  <Boolean key="Part_Pig_18_SET" value="True" />
  <Boolean key="Part_Pig_18_SET_isNew" value="False" />
  <Boolean key="Part_Pig_18_SET_isUsed" value="True" />
  <Boolean key="Part_SpotLight_01_SET_isUsed" value="True" />
  <Boolean key="Part_PointLight_01_SET_isUsed" value="True" />
  <Boolean key="Part_GoldenPig_01_SET_isUsed" value="True" />
  <Boolean key="Part_Gearbox_01_SET_isUsed" value="True" />
  <Boolean key="Part_Kicker_isUsed" value="True" />
  <Boolean key="Part_GrapplingHook_01_SET_isUsed" value="True" />
  <Boolean key="Part_StickyWheel_01_SET_isUsed" value="True" />
  <Boolean key="Part_SpringBoxingGlove_01_SET_isUsed" value="True" />
  <Boolean key="Part_MetalTail_01_SET_isUsed" value="True" />
  <Boolean key="Part_MetalWings_01_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenTail_01_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenWings_01_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags3_01_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbags2_01_SET_isUsed" value="True" />
  <Boolean key="Part_Sandbag_01_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons3_01_SET_isUsed" value="True" />
  <Boolean key="Part_Balloons2_01_SET_isUsed" value="True" />
  <Boolean key="Part_Balloon_01_SET_isUsed" value="True" />
  <Boolean key="Part_Rope_01_SET_isUsed" value="True" />
  <Boolean key="Part_TNT_01_SET_isUsed" value="True" />
  <Boolean key="Part_Spring_01_SET_isUsed" value="True" />
  <Boolean key="Part_PoweredUmbrella_01_SET_isUsed" value="True" />
  <Boolean key="Part_Umbrella_01_SET_isUsed" value="True" />
  <Boolean key="Part_EngineBig_01_SET_isUsed" value="True" />
  <Boolean key="Part_Engine_01_SET_isUsed" value="True" />
  <Boolean key="Part_EngineSmall_01_SET_isUsed" value="True" />
  <Boolean key="Part_RedRocket_01_SET_isUsed" value="True" />
  <Boolean key="Part_Rocket_01_SET_isUsed" value="True" />
  <Boolean key="Part_SodaBottle_01_SET_isUsed" value="True" />
  <Boolean key="Part_CokeBottle_01_SET_isUsed" value="True" />
  <Boolean key="Part_Rotor_01_SET_isUsed" value="True" />
  <Boolean key="Part_PlanePropeller_01_SET_isUsed" value="True" />
  <Boolean key="Part_Fan_01_SET_isUsed" value="True" />
  <Boolean key="Part_Bellows_01_SET_isUsed" value="True" />
  <Boolean key="Part_MotorWheel_01_SET_isUsed" value="True" />
  <Boolean key="Part_SmallWheel_01_SET_isUsed" value="True" />
  <Boolean key="Part_NormalWheel_01_SET_isUsed" value="True" />
  <Boolean key="Part_CartWheel_01_SET_isUsed" value="True" />
  <Boolean key="Part_MetalFrame_01_SET_isUsed" value="True" />
  <Boolean key="Part_WoodenFrame_01_SET_isUsed" value="True" />
  <Boolean key="Part_Egg_01_SET_isUsed" value="True" />
  <Boolean key="CakeRaceUnlockShown" value="True" />
  <Int32 key="Blueprints_Available" value="100003" />
  <Boolean key="Level_05_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_05" value="1" />
  <Int32 key="Level_05_contraption" value="1" />
  <Int32 key="Level_05_challenge_0" value="2" />
  <Int32 key="Level_05_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_05" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_05" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_05" value="1" />
  <Int32 key="Level_05_stars" value="3" />
  <Int32 key="StartedLevel test28" value="1" />
  <Int32 key="test28_contraption" value="1" />
  <Int32 key="test28_challenge_0" value="2" />
  <Int32 key="test28_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest28" value="1" />
  <Int32 key="exp_LevelComplete2Startest28" value="1" />
  <Int32 key="exp_LevelComplete3Startest28" value="1" />
  <Int32 key="test28_stars" value="3" />
  <Int32 key="StartedLevel Level_20" value="1" />
  <Int32 key="Level_20_contraption" value="1" />
  <Int32 key="Level_20_challenge_0" value="2" />
  <Int32 key="Level_20_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_20" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_20" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_20" value="1" />
  <Int32 key="Level_20_stars" value="3" />
  <Int32 key="StartedLevel Level_49" value="1" />
  <Int32 key="Level_49_contraption" value="1" />
  <Int32 key="Level_49_challenge_0" value="2" />
  <Int32 key="Level_49_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_49" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_49" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_49" value="1" />
  <Int32 key="Level_49_stars" value="3" />
  <Int32 key="StartedLevel test02" value="1" />
  <Int32 key="test02_contraption" value="1" />
  <Int32 key="test02_challenge_0" value="2" />
  <Int32 key="test02_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest02" value="1" />
  <Int32 key="exp_LevelComplete2Startest02" value="1" />
  <Int32 key="exp_LevelComplete3Startest02" value="1" />
  <Int32 key="test02_stars" value="3" />
  <Int32 key="StartedLevel Level_22" value="1" />
  <Int32 key="Level_22_contraption" value="1" />
  <Int32 key="Level_22_challenge_0" value="2" />
  <Int32 key="Level_22_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_22" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_22" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_22" value="1" />
  <Int32 key="Level_22_stars" value="3" />
  <Int32 key="StartedLevel test05" value="1" />
  <Int32 key="test05_contraption" value="1" />
  <Int32 key="test05_challenge_0" value="2" />
  <Int32 key="test05_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest05" value="1" />
  <Int32 key="exp_LevelComplete2Startest05" value="1" />
  <Int32 key="exp_LevelComplete3Startest05" value="1" />
  <Int32 key="test05_stars" value="3" />
  <Boolean key="test51_Rotation_Tutorial_Completed" value="True" />
  <Int32 key="StartedLevel test51" value="1" />
  <Int32 key="test51_contraption" value="1" />
  <Int32 key="test51_challenge_0" value="2" />
  <Int32 key="test51_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest51" value="1" />
  <Int32 key="exp_LevelComplete2Startest51" value="1" />
  <Int32 key="exp_LevelComplete3Startest51" value="1" />
  <Int32 key="test51_stars" value="3" />
  <Int32 key="StartedLevel test31" value="1" />
  <Int32 key="test31_contraption" value="1" />
  <Int32 key="test31_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest31" value="1" />
  <Int32 key="exp_LevelComplete2Startest31" value="1" />
  <Int32 key="exp_LevelComplete3Startest31" value="1" />
  <Int32 key="test31_stars" value="3" />
  <Int32 key="StartedLevel Level_17" value="1" />
  <Int32 key="Level_17_contraption" value="1" />
  <Int32 key="Level_17_challenge_0" value="2" />
  <Int32 key="Level_17_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_17" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_17" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_17" value="1" />
  <Int32 key="Level_17_stars" value="3" />
  <Int32 key="StartedLevel test11" value="1" />
  <Int32 key="test11_contraption" value="1" />
  <Int32 key="test11_challenge_0" value="2" />
  <Int32 key="test11_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest11" value="1" />
  <Int32 key="exp_LevelComplete2Startest11" value="1" />
  <Int32 key="exp_LevelComplete3Startest11" value="1" />
  <Int32 key="test11_stars" value="3" />
  <Int32 key="StartedLevel Level_24" value="1" />
  <Int32 key="Level_24_contraption" value="1" />
  <Int32 key="Level_24_challenge_0" value="2" />
  <Int32 key="Level_24_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_24" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_24" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_24" value="1" />
  <Int32 key="Level_24_stars" value="3" />
  <Int32 key="StartedLevel Level_25" value="1" />
  <Int32 key="Level_25_contraption" value="1" />
  <Int32 key="Level_25_challenge_0" value="2" />
  <Int32 key="Level_25_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_25" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_25" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_25" value="1" />
  <Int32 key="Level_25_stars" value="3" />
  <Int32 key="StartedLevel Level_14" value="1" />
  <Int32 key="Level_14_contraption" value="1" />
  <Boolean key="Level_14_autobuild_available" value="True" />
  <Int32 key="Level_14_challenge_0" value="2" />
  <Int32 key="Level_14_challenge_1" value="2" />
  <Int32 key="Level_14_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_14" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_14" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_14" value="1" />
  <Int32 key="Level_14_stars" value="3" />
  <Boolean key="test13_autobuild_available" value="True" />
  <Int32 key="StartedLevel test13" value="1" />
  <Int32 key="test13_contraption" value="1" />
  <Int32 key="test13_challenge_0" value="2" />
  <Int32 key="test13_challenge_1" value="2" />
  <Int32 key="test13_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest13" value="1" />
  <Int32 key="exp_LevelComplete2Startest13" value="1" />
  <Int32 key="exp_LevelComplete3Startest13" value="1" />
  <Int32 key="test13_stars" value="3" />
  <Boolean key="Level_26_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_26" value="1" />
  <Int32 key="Level_26_contraption" value="1" />
  <Int32 key="Level_26_challenge_0" value="2" />
  <Int32 key="Level_26_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_26" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_26" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_26" value="1" />
  <Int32 key="Level_26_stars" value="3" />
  <Boolean key="Level_15_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_15" value="1" />
  <Int32 key="Level_15_contraption" value="1" />
  <Int32 key="Level_15_challenge_0" value="2" />
  <Int32 key="Level_15_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_15" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_15" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_15" value="1" />
  <Int32 key="Level_15_stars" value="3" />
  <Boolean key="test21_autobuild_available" value="True" />
  <Int32 key="StartedLevel test21" value="1" />
  <Int32 key="test21_contraption" value="1" />
  <Boolean key="CollectedFirstLootCrate" value="True" />
  <Int32 key="Crate_amount_Glass" value="0" />
  <Int32 key="Glass_crates_collected" value="28" />
  <Int32 key="test21_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest21" value="1" />
  <Int32 key="exp_LevelComplete2Startest21" value="1" />
  <Int32 key="exp_LevelComplete3Startest21" value="1" />
  <Int32 key="test21_stars" value="3" />
  <Int32 key="StartedLevel Level_18" value="1" />
  <Int32 key="Level_18_contraption" value="1" />
  <Int32 key="Level_18_challenge_0" value="2" />
  <Int32 key="Level_18_challenge_1" value="2" />
  <Int32 key="Level_18_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_18" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_18" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_18" value="1" />
  <Int32 key="Level_18_stars" value="3" />
  <Boolean key="test35_autobuild_available" value="True" />
  <Int32 key="StartedLevel test35" value="1" />
  <Int32 key="test35_contraption" value="1" />
  <Int32 key="test35_challenge_0" value="2" />
  <Int32 key="test35_challenge_1" value="2" />
  <Int32 key="test35_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest35" value="1" />
  <Int32 key="exp_LevelComplete2Startest35" value="1" />
  <Int32 key="exp_LevelComplete3Startest35" value="1" />
  <Int32 key="test35_stars" value="3" />
  <Boolean key="test39_autobuild_available" value="True" />
  <Int32 key="StartedLevel test39" value="1" />
  <Int32 key="test39_contraption" value="1" />
  <Int32 key="test39_challenge_0" value="2" />
  <Int32 key="test39_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest39" value="1" />
  <Int32 key="exp_LevelComplete2Startest39" value="1" />
  <Int32 key="exp_LevelComplete3Startest39" value="1" />
  <Int32 key="test39_stars" value="3" />
  <Boolean key="test40_autobuild_available" value="True" />
  <Int32 key="StartedLevel test40" value="1" />
  <Int32 key="test40_contraption" value="1" />
  <Int32 key="test40_challenge_0" value="2" />
  <Int32 key="test40_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest40" value="1" />
  <Int32 key="exp_LevelComplete2Startest40" value="1" />
  <Int32 key="exp_LevelComplete3Startest40" value="1" />
  <Int32 key="test40_stars" value="3" />
  <Boolean key="test36_autobuild_available" value="True" />
  <Int32 key="StartedLevel test36" value="1" />
  <Int32 key="test36_contraption" value="1" />
  <Int32 key="test36_challenge_0" value="2" />
  <Int32 key="test36_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest36" value="1" />
  <Int32 key="exp_LevelComplete2Startest36" value="1" />
  <Int32 key="exp_LevelComplete3Startest36" value="1" />
  <Int32 key="test36_stars" value="3" />
  <Boolean key="DailyChallengeCutscene" value="False" />
  <Int32 key="DailyChallenge_played" value="1" />
  <Boolean key="DailyChallengeShown" value="True" />
  <Boolean key="UnlockShown_CakeRaceButton" value="True" />
  <Boolean key="CakeRaceIntroShown" value="True" />
  <Int32 key="CakeRaceIntro_played" value="1" />
  <Boolean key="FacebookConnectDialogShown" value="True" />
  <Boolean key="CakeRaceStartTutorialShown" value="True" />
  <Int32 key="cake_race_current_week" value="151" />
  <Boolean key="cake_race_fte_event" value="True" />
  <String key="cake_race_first_day" value="12/31/2019" />
  <String key="cake_race_last_played" value="01/04/2020" />
  <Int32 key="StartedLevel Level_Sandbox_02" value="1" />
  <Int32 key="cr_Level_Sandbox_02_contraption_0" value="1" />
  <Int32 key="loot_crates_added_to_slots" value="25" />
  <String key="cake_race_track_0_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;S-2_0&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;5000&quot;,&quot;1&quot;:&quot;5000&quot;,&quot;2&quot;:&quot;5000&quot;,&quot;3&quot;:&quot;5000&quot;,&quot;4&quot;:&quot;5000&quot;}}" />
  <Int32 key="cake_race_total_wins" value="77" />
  <Int32 key="Season_0151_2019_wins" value="17" />
  <Boolean key="LootCrateTutorialShown" value="True" />
  <Boolean key="BeginOpeninTutorialShown" value="True" />
  <Int32 key="cake_race_days_played" value="67" />
  <Int32 key="StartedLevel Level_Race_01" value="1" />
  <Int32 key="cr_Level_Race_01_contraption_0" value="1" />
  <Int32 key="StartedLevel Level_Race_08" value="1" />
  <String key="cake_race_track_1_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;R-4_0&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;4000&quot;,&quot;1&quot;:&quot;4000&quot;,&quot;2&quot;:&quot;4000&quot;,&quot;3&quot;:&quot;4000&quot;,&quot;4&quot;:&quot;4000&quot;}}" />
  <Int32 key="loot_crates_unlocked_from_slots" value="27" />
  <Int32 key="cr_Level_Race_08_contraption_0" value="1" />
  <Int32 key="Metal_crates_collected" value="20" />
  <String key="cake_race_track_2_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;R-8_0&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;3000&quot;,&quot;1&quot;:&quot;3000&quot;,&quot;2&quot;:&quot;3000&quot;,&quot;3&quot;:&quot;3000&quot;,&quot;4&quot;:&quot;3000&quot;}}" />
  <Boolean key="ChiefPigExploded" value="True" />
  <Int32 key="StrawberryCake" value="10004" />
  <Int32 key="TotalDessertCount" value="1136" />
  <Int32 key="VanillaCakeSlice" value="10000" />
  <Int32 key="Cupcake" value="10000" />
  <Int32 key="IcecreamBalls" value="10000" />
  <Int32 key="CreamyBun" value="10009" />
  <Boolean key="Kingpig_Visited" value="True" />
  <Int32 key="EatenDessertsCount" value="97" />
  <Single key="KingPigFeedScale" value="4" />
  <Int32 key="LastDessertCount" value="59994" />
  <String key="test22_dessert_placement" value="DessertPlace03:CreamyBun;DessertPlace02:Cupcake" />
  <Boolean key="test22_autobuild_available" value="True" />
  <Int32 key="StartedLevel test22" value="1" />
  <Int32 key="test22_contraption" value="1" />
  <Int32 key="test22_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest22" value="1" />
  <Int32 key="exp_LevelComplete2Startest22" value="1" />
  <Int32 key="exp_LevelComplete3Startest22" value="1" />
  <Int32 key="test22_stars" value="3" />
  <String key="test25_dessert_placement" value="DessertPlace01:Cupcake;DessertPlace03:Cupcake" />
  <Boolean key="test25_autobuild_available" value="True" />
  <Int32 key="StartedLevel test25" value="1" />
  <Int32 key="test25_contraption" value="1" />
  <Int32 key="test25_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest25" value="1" />
  <Int32 key="exp_LevelComplete2Startest25" value="1" />
  <Int32 key="exp_LevelComplete3Startest25" value="1" />
  <Int32 key="test25_stars" value="3" />
  <String key="test26_dessert_placement" value="DessertPlace03:Cupcake" />
  <Int32 key="Statistics_CakeRaceCupF2" value="5580000" />
  <Int32 key="Statistics_CakeRaceCupF2_Version" value="347" />
  <String key="episode_6_level_16_dessert_placement" value="DessertPlace09:IcecreamBalls;DessertPlace01:CreamyBun" />
  <Int32 key="button_unlock_RaceLevelButton_R-1" value="2" />
  <Boolean key="leaderboard_opened" value="True" />
  <Boolean key="test26_autobuild_available" value="True" />
  <Int32 key="StartedLevel test26" value="1" />
  <Int32 key="test26_contraption" value="1" />
  <Int32 key="test26_challenge_0" value="2" />
  <Int32 key="test26_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest26" value="1" />
  <Int32 key="exp_LevelComplete2Startest26" value="1" />
  <Int32 key="exp_LevelComplete3Startest26" value="1" />
  <Int32 key="test26_stars" value="3" />
  <String key="test23_dessert_placement" value="" />
  <Boolean key="test23_autobuild_available" value="True" />
  <Int32 key="StartedLevel test23" value="1" />
  <Int32 key="test23_contraption" value="1" />
  <Int32 key="test23_challenge_0" value="2" />
  <Int32 key="test23_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest23" value="1" />
  <Int32 key="exp_LevelComplete2Startest23" value="1" />
  <Int32 key="exp_LevelComplete3Startest23" value="1" />
  <Int32 key="test23_stars" value="3" />
  <String key="test41_dessert_placement" value="" />
  <Boolean key="test41_autobuild_available" value="True" />
  <Int32 key="StartedLevel test41" value="1" />
  <Int32 key="test41_contraption" value="1" />
  <Int32 key="test41_challenge_0" value="2" />
  <Int32 key="test41_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest41" value="1" />
  <Int32 key="exp_LevelComplete2Startest41" value="1" />
  <Int32 key="exp_LevelComplete3Startest41" value="1" />
  <Int32 key="test41_stars" value="3" />
  <String key="test43_dessert_placement" value="DessertPlace10:IcecreamBalls;DessertPlace13:Cupcake" />
  <Boolean key="test43_autobuild_available" value="True" />
  <Int32 key="StartedLevel test43" value="1" />
  <Int32 key="test43_contraption" value="1" />
  <Int32 key="test43_challenge_0" value="2" />
  <Int32 key="test43_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest43" value="1" />
  <Int32 key="exp_LevelComplete2Startest43" value="1" />
  <Int32 key="exp_LevelComplete3Startest43" value="1" />
  <Int32 key="test43_stars" value="3" />
  <String key="test44_dessert_placement" value="" />
  <Boolean key="test44_autobuild_available" value="True" />
  <Int32 key="StartedLevel test44" value="1" />
  <Int32 key="test44_contraption" value="1" />
  <Int32 key="test44_challenge_0" value="2" />
  <Int32 key="test44_challenge_1" value="2" />
  <Int32 key="test44_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest44" value="1" />
  <Int32 key="exp_LevelComplete2Startest44" value="1" />
  <Int32 key="exp_LevelComplete3Startest44" value="1" />
  <Int32 key="test44_stars" value="3" />
  <String key="test45_dessert_placement" value="" />
  <Boolean key="test45_autobuild_available" value="True" />
  <Int32 key="StartedLevel test45" value="1" />
  <Int32 key="test45_contraption" value="1" />
  <Int32 key="test45_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest45" value="1" />
  <Int32 key="exp_LevelComplete2Startest45" value="1" />
  <Int32 key="exp_LevelComplete3Startest45" value="1" />
  <Int32 key="test45_stars" value="3" />
  <String key="Level_30_dessert_placement" value="" />
  <Boolean key="Level_30_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_30" value="1" />
  <Int32 key="Level_30_contraption" value="1" />
  <Int32 key="Level_30_challenge_0" value="2" />
  <Int32 key="Level_30_challenge_1" value="2" />
  <Int32 key="Level_30_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_30" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_30" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_30" value="1" />
  <Int32 key="Level_30_stars" value="3" />
  <String key="test47_dessert_placement" value="" />
  <Boolean key="test47_autobuild_available" value="True" />
  <Int32 key="StartedLevel test47" value="1" />
  <Int32 key="test47_contraption" value="1" />
  <Int32 key="test47_challenge_0" value="2" />
  <Int32 key="test47_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest47" value="1" />
  <Int32 key="exp_LevelComplete2Startest47" value="1" />
  <Int32 key="exp_LevelComplete3Startest47" value="1" />
  <Int32 key="test47_stars" value="3" />
  <String key="Level_31_dessert_placement" value="DessertPlace01:VanillaCakeSlice" />
  <Boolean key="Level_31_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_31" value="1" />
  <Int32 key="Level_31_contraption" value="1" />
  <Int32 key="Level_31_challenge_0" value="2" />
  <Int32 key="Level_31_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_31" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_31" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_31" value="1" />
  <Int32 key="Level_31_stars" value="3" />
  <String key="Level_32_dessert_placement" value="" />
  <Boolean key="Level_32_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_32" value="1" />
  <Int32 key="Level_32_contraption" value="1" />
  <Int32 key="Level_32_challenge_0" value="2" />
  <Int32 key="Level_32_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_32" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_32" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_32" value="1" />
  <Int32 key="Level_32_stars" value="3" />
  <Int32 key="Episode1_End_played" value="1" />
  <Int32 key="GoldenCake" value="10000" />
  <String key="Level_23_dessert_placement" value="DessertPlace13:StrawberryCake" />
  <Boolean key="Level_23_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_23" value="1" />
  <Int32 key="Level_23_contraption" value="1" />
  <Int32 key="Level_23_challenge_0" value="2" />
  <Int32 key="Level_23_challenge_1" value="2" />
  <Int32 key="Level_23_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_23" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_23" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_23" value="1" />
  <Int32 key="Level_23_stars" value="3" />
  <String key="test29_dessert_placement" value="DessertPlace27:Cupcake;DessertPlace29:StrawberryCake" />
  <Boolean key="test29_autobuild_available" value="True" />
  <Int32 key="StartedLevel test29" value="1" />
  <Int32 key="test29_contraption" value="1" />
  <Int32 key="test29_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest29" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest29" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest29" value="1" />
  <Int32 key="test29_stars" value="3" />
  <String key="test33_dessert_placement" value="DessertPlace39:Cupcake;DessertPlace14:StrawberryCake" />
  <Boolean key="test33_autobuild_available" value="True" />
  <Int32 key="StartedLevel test33" value="1" />
  <Int32 key="test33_contraption" value="1" />
  <Int32 key="test33_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest33" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest33" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest33" value="1" />
  <Int32 key="test33_stars" value="3" />
  <String key="Level_27_dessert_placement" value="DessertPlace21:Cupcake;DessertPlace22:StrawberryCake" />
  <Boolean key="Level_27_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_27" value="1" />
  <Int32 key="Level_27_contraption" value="1" />
  <Int32 key="Level_27_challenge_0" value="2" />
  <Int32 key="Level_27_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_27" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_27" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_27" value="1" />
  <Int32 key="Level_27_stars" value="3" />
  <String key="test34_dessert_placement" value="DessertPlace03:VanillaCakeSlice" />
  <Boolean key="test34_autobuild_available" value="True" />
  <Int32 key="StartedLevel test34" value="1" />
  <Int32 key="test34_contraption" value="1" />
  <Int32 key="test34_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest34" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest34" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest34" value="1" />
  <Int32 key="test34_stars" value="3" />
  <String key="test37_dessert_placement" value="DessertPlace20:IcecreamBalls" />
  <Boolean key="test37_autobuild_available" value="True" />
  <Int32 key="StartedLevel test37" value="1" />
  <Int32 key="test37_contraption" value="1" />
  <Int32 key="test37_challenge_0" value="2" />
  <Int32 key="test37_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest37" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest37" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest37" value="1" />
  <Int32 key="test37_stars" value="3" />
  <String key="Level_29_dessert_placement" value="DessertPlace15:StrawberryCake" />
  <Boolean key="Level_29_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_29" value="1" />
  <Int32 key="Level_29_contraption" value="1" />
  <Int32 key="Level_29_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_29" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_29" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_29" value="1" />
  <Int32 key="Level_29_stars" value="3" />
  <String key="test42_dessert_placement" value="DessertPlace21:CreamyBun" />
  <Boolean key="test42_autobuild_available" value="True" />
  <Int32 key="StartedLevel test42" value="1" />
  <Int32 key="test42_contraption" value="1" />
  <Int32 key="test42_challenge_0" value="2" />
  <Int32 key="test42_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest42" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest42" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest42" value="1" />
  <Int32 key="test42_stars" value="3" />
  <String key="Level_33_dessert_placement" value="DessertPlace01:VanillaCakeSlice;DessertPlace29:IcecreamBalls;DessertPlace23:VanillaCakeSlice;DessertPlace17:StrawberryCake" />
  <Boolean key="Level_33_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_33" value="1" />
  <Int32 key="Level_33_contraption" value="1" />
  <Int32 key="Level_33_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_33" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_33" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_33" value="1" />
  <Int32 key="Level_33_stars" value="3" />
  <Int32 key="NightVisions_Available" value="100000" />
  <String key="Level_21_dessert_placement" value="DessertPlace02:IcecreamBalls" />
  <Boolean key="FirstChallengeCollected" value="True" />
  <Int32 key="Crate_amount_Cardboard" value="0" />
  <Int32 key="Cardboard_crates_collected" value="27" />
  <Int32 key="cr_Level_Race_01_contraption_4" value="1" />
  <Int32 key="Crate_amount_Metal" value="0" />
  <String key="cake_race_track_3_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;R-4_4&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;5000&quot;,&quot;1&quot;:&quot;5000&quot;,&quot;2&quot;:&quot;5000&quot;,&quot;3&quot;:&quot;5000&quot;,&quot;4&quot;:&quot;5000&quot;}}" />
  <Int32 key="cr_Level_Race_01_contraption_3" value="1" />
  <String key="cake_race_track_4_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;R-4_3&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;4000&quot;,&quot;1&quot;:&quot;4000&quot;,&quot;2&quot;:&quot;4000&quot;,&quot;3&quot;:&quot;4000&quot;,&quot;4&quot;:&quot;4000&quot;}}" />
  <Int32 key="StartedLevel Episode_6_Tower Sandbox" value="1" />
  <Int32 key="cr_Episode_6_Tower Sandbox_contraption_1" value="1" />
  <String key="cake_race_track_5_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;S-9_1&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;0&quot;:&quot;5000&quot;,&quot;1&quot;:&quot;5000&quot;,&quot;2&quot;:&quot;5000&quot;,&quot;3&quot;:&quot;5000&quot;,&quot;4&quot;:&quot;5000&quot;}}" />
  <Int32 key="button_unlock_RaceLevelButton_R-8" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-5" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-4" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-6" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-3" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-2" value="1" />
  <Int32 key="button_unlock_RaceLevelButton_R-7" value="1" />
  <Int32 key="Episode2a_Start_played" value="1" />
  <String key="scenario_69_dessert_placement" value="" />
  <Int32 key="StartedLevel scenario_69" value="1" />
  <Int32 key="scenario_69_contraption" value="1" />
  <Int32 key="scenario_69_challenge_0" value="2" />
  <Int32 key="scenario_69_challenge_1" value="2" />
  <Int32 key="scenario_69_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_69" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_69" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_69" value="1" />
  <Int32 key="scenario_69_stars" value="3" />
  <String key="scenario_70_dessert_placement" value="" />
  <Int32 key="StartedLevel scenario_70" value="1" />
  <Int32 key="scenario_70_contraption" value="1" />
  <Int32 key="scenario_70_challenge_0" value="2" />
  <Int32 key="scenario_70_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_70" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_70" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_70" value="1" />
  <Int32 key="scenario_70_stars" value="3" />
  <String key="scenario_73_dessert_placement" value="" />
  <Int32 key="StartedLevel scenario_73" value="1" />
  <Int32 key="scenario_73_contraption" value="1" />
  <Int32 key="scenario_73_challenge_0" value="2" />
  <Int32 key="scenario_73_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_73" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_73" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_73" value="1" />
  <Int32 key="scenario_73_stars" value="3" />
  <String key="scenario_71_dessert_placement" value="" />
  <Int32 key="StartedLevel scenario_71" value="1" />
  <Int32 key="scenario_71_contraption" value="1" />
  <Int32 key="scenario_71_challenge_0" value="2" />
  <Int32 key="scenario_71_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_71" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_71" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_71" value="1" />
  <Int32 key="scenario_71_stars" value="3" />
  <String key="scenario_59_dessert_placement" value="DessertPlace02:Cupcake" />
  <Boolean key="scenario_59_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_59" value="1" />
  <Int32 key="scenario_59_contraption" value="1" />
  <Int32 key="scenario_59_challenge_0" value="2" />
  <Int32 key="scenario_59_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_59" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_59" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_59" value="1" />
  <Int32 key="scenario_59_stars" value="3" />
  <String key="scenario_60_dessert_placement" value="" />
  <Boolean key="scenario_60_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_60" value="1" />
  <Int32 key="scenario_60_contraption" value="1" />
  <Int32 key="scenario_60_challenge_0" value="2" />
  <Int32 key="scenario_60_challenge_1" value="2" />
  <Int32 key="scenario_60_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_60" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_60" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_60" value="1" />
  <Int32 key="scenario_60_stars" value="3" />
  <String key="scenario_61_dessert_placement" value="" />
  <Boolean key="scenario_61_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_61" value="1" />
  <Int32 key="scenario_61_contraption" value="1" />
  <Int32 key="scenario_61_challenge_0" value="2" />
  <Int32 key="scenario_61_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_61" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_61" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_61" value="1" />
  <Int32 key="scenario_61_stars" value="3" />
  <String key="scenario_63_dessert_placement" value="DessertPlace08:CreamyBun;DessertPlace01:Cupcake" />
  <Int32 key="Level_Sandbox_06_contraption_1" value="1" />
  <String key="LootCrateSlot_0" value="Inactive,Glass" />
  <Int32 key="LootCrateSlot_3_date" value="1578141554" />
  <String key="LootCrateSlotOpening" value="LootCrateSlot_3" />
  <Boolean key="SECRET_DISCOVERED_scenario_27" value="True" />
  <String key="test03_dessert_placement" value="DessertPlace05:StrawberryCake;DessertPlace04:VanillaCakeSlice" />
  <String key="Level_36_dessert_placement" value="DessertPlace03:CreamyBun" />
  <String key="Level_Sandbox_04_dessert_placement" value="DessertPlace14:Cupcake;DessertPlace58:CreamyBun;DessertPlace36:StrawberryCake;DessertPlace56:Cupcake;DessertPlace24:CreamyBun;DessertPlace11:VanillaCakeSlice;DessertPlace46:StrawberryCake;DessertPlace42:IcecreamBalls;DessertPlace15:IcecreamBalls;DessertPlace25:CreamyBun" />
  <Int32 key="Level_Sandbox_04_star_StarBox18" value="2" />
  <Boolean key="scenario_63_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_63" value="1" />
  <Int32 key="scenario_63_contraption" value="1" />
  <Int32 key="scenario_63_challenge_0" value="2" />
  <Int32 key="scenario_63_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_63" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_63" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_63" value="1" />
  <Int32 key="scenario_63_stars" value="3" />
  <String key="course_02_dessert_placement" value="DessertPlace14:IcecreamBalls" />
  <Boolean key="course_02_autobuild_available" value="True" />
  <Int32 key="StartedLevel course_02" value="1" />
  <Int32 key="course_02_contraption" value="1" />
  <Int32 key="course_02_challenge_0" value="2" />
  <Int32 key="course_02_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starcourse_02" value="1" />
  <Int32 key="exp_LevelComplete2Starcourse_02" value="1" />
  <Int32 key="exp_LevelComplete3Starcourse_02" value="1" />
  <Int32 key="course_02_stars" value="3" />
  <String key="scenario_75_dessert_placement" value="" />
  <Boolean key="scenario_75_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_75" value="1" />
  <Int32 key="scenario_75_contraption" value="1" />
  <Int32 key="scenario_75_challenge_0" value="2" />
  <Int32 key="scenario_75_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_75" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_75" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_75" value="1" />
  <Int32 key="scenario_75_stars" value="3" />
  <String key="scenario_72_dessert_placement" value="" />
  <Boolean key="scenario_72_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_72" value="1" />
  <Int32 key="scenario_72_contraption" value="1" />
  <Int32 key="scenario_72_challenge_0" value="2" />
  <Int32 key="scenario_72_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_72" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_72" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_72" value="1" />
  <Int32 key="scenario_72_stars" value="3" />
  <String key="track_21_dessert_placement" value="DessertPlace07:Cupcake" />
  <Boolean key="track_21_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_21" value="1" />
  <Int32 key="track_21_contraption" value="1" />
  <Int32 key="track_21_challenge_0" value="2" />
  <Int32 key="track_21_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_21" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_21" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_21" value="1" />
  <Int32 key="track_21_stars" value="3" />
  <String key="scenario_85_dessert_placement" value="" />
  <Boolean key="scenario_85_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_85" value="1" />
  <Int32 key="scenario_85_contraption" value="1" />
  <Int32 key="scenario_85_challenge_0" value="2" />
  <Int32 key="scenario_85_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_85" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_85" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_85" value="1" />
  <Int32 key="scenario_85_stars" value="3" />
  <String key="scenario_88_dessert_placement" value="" />
  <Boolean key="scenario_88_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_88" value="1" />
  <Int32 key="scenario_88_contraption" value="1" />
  <Int32 key="scenario_88_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_88" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_88" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_88" value="1" />
  <Int32 key="scenario_88_stars" value="3" />
  <String key="scenario_91_dessert_placement" value="" />
  <Boolean key="scenario_91_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_91" value="1" />
  <Int32 key="scenario_91_contraption" value="1" />
  <Int32 key="scenario_91_challenge_0" value="2" />
  <Int32 key="scenario_91_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_91" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_91" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_91" value="1" />
  <Int32 key="scenario_91_stars" value="3" />
  <String key="scenario_94_dessert_placement" value="DessertPlace05:IcecreamBalls" />
  <Boolean key="scenario_94_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_94" value="1" />
  <Int32 key="scenario_94_contraption" value="1" />
  <Int32 key="scenario_94_challenge_0" value="2" />
  <Int32 key="scenario_94_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_94" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_94" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_94" value="1" />
  <Int32 key="scenario_94_stars" value="3" />
  <String key="scenario_86_dessert_placement" value="" />
  <Boolean key="scenario_86_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_86" value="1" />
  <Int32 key="scenario_86_contraption" value="1" />
  <Int32 key="scenario_86_challenge_0" value="2" />
  <Int32 key="scenario_86_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_86" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_86" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_86" value="1" />
  <Int32 key="scenario_86_stars" value="3" />
  <String key="scenario_87_dessert_placement" value="" />
  <Boolean key="scenario_87_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_87" value="1" />
  <Int32 key="scenario_87_contraption" value="1" />
  <Int32 key="scenario_87_challenge_0" value="2" />
  <Int32 key="scenario_87_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_87" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_87" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_87" value="1" />
  <Int32 key="scenario_87_stars" value="3" />
  <String key="scenario_92_dessert_placement" value="" />
  <Boolean key="scenario_92_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_92" value="1" />
  <Int32 key="scenario_92_contraption" value="1" />
  <Int32 key="scenario_92_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_92" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_92" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_92" value="1" />
  <Int32 key="scenario_92_stars" value="3" />
  <String key="scenario_90_dessert_placement" value="" />
  <Boolean key="scenario_90_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_90" value="1" />
  <Int32 key="scenario_90_contraption" value="1" />
  <Int32 key="scenario_90_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_90" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_90" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_90" value="1" />
  <Int32 key="scenario_90_stars" value="3" />
  <String key="scenario_58_dessert_placement" value="" />
  <Boolean key="scenario_58_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_58" value="1" />
  <Int32 key="scenario_58_contraption" value="1" />
  <Int32 key="scenario_58_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_58" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_58" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_58" value="1" />
  <Int32 key="scenario_58_stars" value="3" />
  <String key="track_14_dessert_placement" value="" />
  <Boolean key="track_14_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_14" value="1" />
  <Int32 key="track_14_contraption" value="1" />
  <Int32 key="track_14_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_14" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_14" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_14" value="1" />
  <Int32 key="track_14_stars" value="3" />
  <String key="track_25_dessert_placement" value="DessertPlace02:IcecreamBalls" />
  <Boolean key="track_25_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_25" value="1" />
  <Int32 key="track_25_contraption" value="1" />
  <Int32 key="track_25_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_25" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_25" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_25" value="1" />
  <Int32 key="track_25_stars" value="3" />
  <String key="course_04_dessert_placement" value="DessertPlace08:CreamyBun" />
  <Boolean key="course_04_autobuild_available" value="True" />
  <Int32 key="StartedLevel course_04" value="1" />
  <Int32 key="course_04_contraption" value="1" />
  <Int32 key="course_04_challenge_0" value="2" />
  <Int32 key="course_04_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starcourse_04" value="1" />
  <Int32 key="exp_LevelComplete2Starcourse_04" value="1" />
  <Int32 key="exp_LevelComplete3Starcourse_04" value="1" />
  <Int32 key="course_04_stars" value="3" />
  <String key="track_20_dessert_placement" value="" />
  <Boolean key="track_20_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_20" value="1" />
  <Int32 key="track_20_contraption" value="1" />
  <Int32 key="track_20_challenge_0" value="2" />
  <Int32 key="track_20_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_20" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_20" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_20" value="1" />
  <Int32 key="track_20_stars" value="3" />
  <String key="scenario_74_dessert_placement" value="" />
  <Boolean key="scenario_74_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_74" value="1" />
  <Int32 key="scenario_74_contraption" value="1" />
  <Int32 key="scenario_74_challenge_0" value="2" />
  <Int32 key="scenario_74_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_74" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_74" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_74" value="1" />
  <Int32 key="scenario_74_stars" value="3" />
  <String key="scenario_82_dessert_placement" value="DessertPlace01:Cupcake" />
  <Boolean key="scenario_82_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_82" value="1" />
  <Int32 key="scenario_82_contraption" value="1" />
  <Int32 key="scenario_82_challenge_0" value="2" />
  <Int32 key="scenario_82_challenge_1" value="2" />
  <Int32 key="scenario_82_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_82" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_82" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_82" value="1" />
  <Int32 key="scenario_82_stars" value="3" />
  <String key="track_31_dessert_placement" value="DessertPlace13:VanillaCakeSlice" />
  <Boolean key="track_31_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_31" value="1" />
  <Int32 key="track_31_contraption" value="1" />
  <Int32 key="track_31_challenge_0" value="2" />
  <Int32 key="track_31_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_31" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_31" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_31" value="1" />
  <Int32 key="track_31_stars" value="3" />
  <String key="track_29_dessert_placement" value="" />
  <Boolean key="track_29_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_29" value="1" />
  <Int32 key="track_29_contraption" value="1" />
  <Int32 key="track_29_challenge_0" value="2" />
  <Int32 key="track_29_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_29" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_29" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_29" value="1" />
  <Int32 key="track_29_stars" value="3" />
  <String key="scenario_67_dessert_placement" value="" />
  <Boolean key="scenario_67_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_67" value="1" />
  <Int32 key="scenario_67_contraption" value="1" />
  <Int32 key="scenario_67_challenge_0" value="2" />
  <Int32 key="scenario_67_challenge_1" value="2" />
  <Int32 key="scenario_67_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_67" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_67" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_67" value="1" />
  <Int32 key="scenario_67_stars" value="3" />
  <String key="scenario_80_dessert_placement" value="" />
  <Boolean key="scenario_80_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_80" value="1" />
  <Int32 key="scenario_80_contraption" value="1" />
  <Int32 key="scenario_80_challenge_0" value="2" />
  <Int32 key="scenario_80_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_80" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_80" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_80" value="1" />
  <Int32 key="scenario_80_stars" value="3" />
  <String key="track_27_dessert_placement" value="" />
  <Boolean key="track_27_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_27" value="1" />
  <Int32 key="track_27_contraption" value="1" />
  <Int32 key="track_27_challenge_0" value="2" />
  <Int32 key="track_27_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_27" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_27" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_27" value="1" />
  <Int32 key="track_27_stars" value="3" />
  <String key="track_28_dessert_placement" value="" />
  <Boolean key="track_28_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_28" value="1" />
  <Int32 key="track_28_contraption" value="1" />
  <Int32 key="track_28_challenge_0" value="2" />
  <Int32 key="track_28_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_28" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_28" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_28" value="1" />
  <Int32 key="track_28_stars" value="3" />
  <String key="scenario_81_dessert_placement" value="" />
  <Boolean key="scenario_81_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_81" value="1" />
  <Int32 key="scenario_81_contraption" value="1" />
  <Int32 key="scenario_81_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_81" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_81" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_81" value="1" />
  <Int32 key="scenario_81_stars" value="3" />
  <String key="track_12_dessert_placement" value="" />
  <Boolean key="track_12_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_12" value="1" />
  <Int32 key="track_12_contraption" value="1" />
  <Int32 key="track_12_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_12" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_12" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_12" value="1" />
  <Int32 key="track_12_stars" value="3" />
  <String key="scenario_79_dessert_placement" value="" />
  <Boolean key="scenario_79_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_79" value="1" />
  <Int32 key="scenario_79_contraption" value="1" />
  <Int32 key="scenario_79_challenge_0" value="2" />
  <Int32 key="scenario_79_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_79" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_79" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_79" value="1" />
  <Int32 key="scenario_79_stars" value="3" />
  <Int32 key="Episode2a_End_played" value="1" />
  <String key="track_18_dessert_placement" value="DessertPlace09:IcecreamBalls" />
  <Boolean key="track_18_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_18" value="1" />
  <Int32 key="track_18_contraption" value="1" />
  <Int32 key="track_18_challenge_0" value="2" />
  <Int32 key="track_18_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startrack_18" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startrack_18" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startrack_18" value="1" />
  <Int32 key="track_18_stars" value="3" />
  <String key="scenario_62_dessert_placement" value="" />
  <Boolean key="scenario_62_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_62" value="1" />
  <Int32 key="scenario_62_contraption" value="1" />
  <Int32 key="scenario_62_challenge_0" value="2" />
  <Int32 key="scenario_62_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_62" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_62" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_62" value="1" />
  <Int32 key="scenario_62_stars" value="3" />
  <String key="track_22_dessert_placement" value="DessertPlace10:Cupcake;DessertPlace12:IcecreamBalls" />
  <Boolean key="track_22_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_22" value="1" />
  <Int32 key="track_22_contraption" value="1" />
  <Int32 key="track_22_challenge_0" value="2" />
  <Int32 key="track_22_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startrack_22" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startrack_22" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startrack_22" value="1" />
  <Int32 key="track_22_stars" value="3" />
  <String key="scenario_93_dessert_placement" value="" />
  <Boolean key="scenario_93_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_93" value="1" />
  <Int32 key="scenario_93_contraption" value="1" />
  <Boolean key="SECRET_DISCOVERED_scenario_93" value="True" />
  <Int32 key="SkullsCollected" value="45" />
  <Int32 key="scenario_93_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_93" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_93" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_93" value="1" />
  <Int32 key="scenario_93_stars" value="3" />
  <String key="scenario_89_dessert_placement" value="" />
  <Boolean key="scenario_89_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_89" value="1" />
  <Int32 key="scenario_89_contraption" value="1" />
  <Int32 key="scenario_89_challenge_0" value="2" />
  <Int32 key="scenario_89_challenge_1" value="2" />
  <Int32 key="scenario_89_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_89" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_89" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_89" value="1" />
  <Int32 key="scenario_89_stars" value="3" />
  <String key="scenario_76_dessert_placement" value="DessertPlace18:CreamyBun;DessertPlace01:StrawberryCake" />
  <Boolean key="scenario_76_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_76" value="1" />
  <Int32 key="scenario_76_contraption" value="1" />
  <Int32 key="scenario_76_challenge_0" value="2" />
  <Int32 key="scenario_76_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_76" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_76" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_76" value="1" />
  <Int32 key="scenario_76_stars" value="3" />
  <String key="REPLAY_LEVEL" value="LevelStub" />
  <String key="scenario_84_dessert_placement" value="DessertPlace15:StrawberryCake;DessertPlace14:Cupcake" />
  <Boolean key="scenario_84_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_84" value="1" />
  <Int32 key="scenario_84_contraption" value="1" />
  <Int32 key="scenario_84_challenge_0" value="2" />
  <Int32 key="scenario_84_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_84" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_84" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_84" value="1" />
  <Int32 key="scenario_84_stars" value="3" />
  <String key="scenario_77_dessert_placement" value="" />
  <Boolean key="scenario_77_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_77" value="1" />
  <Int32 key="scenario_77_contraption" value="1" />
  <Int32 key="scenario_77_challenge_0" value="2" />
  <Int32 key="scenario_77_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_77" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_77" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_77" value="1" />
  <Int32 key="scenario_77_stars" value="3" />
  <String key="scenario_65_dessert_placement" value="" />
  <Boolean key="scenario_65_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_65" value="1" />
  <Int32 key="scenario_65_contraption" value="1" />
  <Int32 key="scenario_65_challenge_0" value="2" />
  <Int32 key="scenario_65_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_65" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_65" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_65" value="1" />
  <Int32 key="scenario_65_stars" value="3" />
  <Boolean key="episode_6_level_16_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_16" value="1" />
  <Int32 key="episode_6_level_16_contraption" value="1" />
  <Int32 key="episode_6_level_16_challenge_0" value="2" />
  <Int32 key="episode_6_level_16_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_16" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_16" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_16" value="1" />
  <Int32 key="episode_6_level_16_stars" value="3" />
  <Int32 key="Crate_amount_Gold" value="0" />
  <Int32 key="Crate_amount_Bronze" value="0" />
  <Int32 key="Crate_amount_Marble" value="0" />
  <Int32 key="Gold_crates_collected" value="15" />
  <Int32 key="Bronze_crates_collected" value="20" />
  <Int32 key="Marble_crates_collected" value="16" />
  <Int32 key="cake_race_total_losses" value="7" />
  <Int32 key="Season_0151_2019_losses" value="1" />
  <Int32 key="cr_Level_Sandbox_04_contraption_2" value="1" />
  <Int32 key="free_creditsMetal" value="1" />
  <Int32 key="StartedLevel Level_Race_07" value="1" />
  <Int32 key="cr_Level_Race_07_contraption_0" value="1" />
  <String key="cake_race_track_6_pb_replay" value="{&quot;uniqueIdentifier&quot;:&quot;R-7_0&quot;,&quot;playerName&quot;:&quot;guest-463153|463153294384&quot;,&quot;playerLevel&quot;:&quot;131&quot;,&quot;kingsFavorite&quot;:&quot;1&quot;,&quot;collectTimes&quot;:{&quot;2&quot;:&quot;5000&quot;,&quot;0&quot;:&quot;5000&quot;,&quot;1&quot;:&quot;5000&quot;,&quot;3&quot;:&quot;5000&quot;,&quot;4&quot;:&quot;5000&quot;}}" />
  <Int32 key="Episode2_Start_played" value="1" />
  <String key="Level_01_dessert_placement" value="" />
  <Int32 key="StartedLevel Level_01" value="1" />
  <Int32 key="Level_01_contraption" value="1" />
  <Int32 key="Level_01_challenge_0" value="2" />
  <Int32 key="Level_01_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_01" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_01" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_01" value="1" />
  <Int32 key="Level_01_stars" value="3" />
  <String key="Level_16_dessert_placement" value="" />
  <Int32 key="StartedLevel Level_16" value="1" />
  <Int32 key="Level_16_contraption" value="1" />
  <Int32 key="Level_16_challenge_0" value="2" />
  <Int32 key="Level_16_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_16" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_16" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_16" value="1" />
  <Int32 key="Level_16_stars" value="3" />
  <String key="Level_02_dessert_placement" value="DessertPlace04:StrawberryCake" />
  <Int32 key="StartedLevel Level_02" value="1" />
  <Int32 key="Level_02_contraption" value="1" />
  <Int32 key="Level_02_challenge_0" value="2" />
  <Int32 key="Level_02_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_02" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_02" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_02" value="1" />
  <Int32 key="Level_02_stars" value="3" />
  <String key="Level_03_dessert_placement" value="" />
  <Int32 key="StartedLevel Level_03" value="1" />
  <Int32 key="Level_03_contraption" value="1" />
  <Int32 key="Level_03_challenge_0" value="2" />
  <Int32 key="Level_03_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_03" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_03" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_03" value="1" />
  <Int32 key="Level_03_stars" value="3" />
  <String key="Level_04_dessert_placement" value="" />
  <Int32 key="StartedLevel Level_04" value="1" />
  <Int32 key="Level_04_contraption" value="1" />
  <Int32 key="Level_04_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_04" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_04" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_04" value="1" />
  <Int32 key="Level_04_stars" value="3" />
  <Boolean key="test03_autobuild_available" value="True" />
  <Int32 key="StartedLevel test03" value="1" />
  <Int32 key="test03_contraption" value="1" />
  <Int32 key="test03_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest03" value="1" />
  <Int32 key="exp_LevelComplete2Startest03" value="1" />
  <Int32 key="exp_LevelComplete3Startest03" value="1" />
  <Int32 key="test03_stars" value="3" />
  <String key="Level_07_dessert_placement" value="" />
  <Boolean key="Level_07_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_07" value="1" />
  <Int32 key="Level_07_contraption" value="1" />
  <Int32 key="Level_07_challenge_0" value="2" />
  <Int32 key="Level_07_challenge_1" value="2" />
  <Int32 key="Level_07_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_07" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_07" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_07" value="1" />
  <Int32 key="Level_07_stars" value="3" />
  <String key="Level_12_dessert_placement" value="" />
  <Boolean key="Level_12_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_12" value="1" />
  <Int32 key="Level_12_contraption" value="1" />
  <Int32 key="Level_12_challenge_0" value="2" />
  <Int32 key="Level_12_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_12" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_12" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_12" value="1" />
  <Int32 key="Level_12_stars" value="3" />
  <String key="test49_dessert_placement" value="DessertPlace09:IcecreamBalls" />
  <Boolean key="test49_autobuild_available" value="True" />
  <Int32 key="StartedLevel test49" value="1" />
  <Int32 key="test49_contraption" value="1" />
  <Int32 key="test49_challenge_0" value="2" />
  <Int32 key="test49_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest49" value="1" />
  <Int32 key="exp_LevelComplete2Startest49" value="1" />
  <Int32 key="exp_LevelComplete3Startest49" value="1" />
  <Int32 key="test49_stars" value="3" />
  <String key="test01_dessert_placement" value="" />
  <Boolean key="test01_autobuild_available" value="True" />
  <Int32 key="StartedLevel test01" value="1" />
  <Int32 key="test01_contraption" value="1" />
  <Int32 key="test01_challenge_0" value="2" />
  <Int32 key="test01_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest01" value="1" />
  <Int32 key="exp_LevelComplete2Startest01" value="1" />
  <Int32 key="exp_LevelComplete3Startest01" value="1" />
  <Int32 key="test01_stars" value="3" />
  <String key="test48_dessert_placement" value="" />
  <Boolean key="test48_autobuild_available" value="True" />
  <Int32 key="StartedLevel test48" value="1" />
  <Int32 key="test48_contraption" value="1" />
  <Boolean key="SECRET_DISCOVERED_test48" value="True" />
  <Int32 key="Season_0151_2020_losses" value="6" />
  <Int32 key="cr_Level_Race_01_contraption_1" value="1" />
  <Int32 key="Season_0151_2020_wins" value="60" />
  <Int32 key="StartedLevel Level_Race_04" value="1" />
  <Int32 key="cr_Level_Race_04_contraption_0" value="1" />
  <Int32 key="test48_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest48" value="1" />
  <Int32 key="exp_LevelComplete2Startest48" value="1" />
  <Int32 key="exp_LevelComplete3Startest48" value="1" />
  <Int32 key="test48_stars" value="3" />
  <String key="Level_11_dessert_placement" value="" />
  <Boolean key="Level_11_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_11" value="1" />
  <Int32 key="Level_11_contraption" value="1" />
  <Int32 key="Level_11_challenge_0" value="2" />
  <Int32 key="Level_11_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_11" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_11" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_11" value="1" />
  <Int32 key="Level_11_stars" value="3" />
  <String key="test14_dessert_placement" value="" />
  <Boolean key="test14_autobuild_available" value="True" />
  <Int32 key="StartedLevel test14" value="1" />
  <Int32 key="test14_contraption" value="1" />
  <Int32 key="test14_challenge_0" value="2" />
  <Int32 key="test14_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest14" value="1" />
  <Int32 key="exp_LevelComplete2Startest14" value="1" />
  <Int32 key="exp_LevelComplete3Startest14" value="1" />
  <Int32 key="test14_stars" value="3" />
  <String key="test17_dessert_placement" value="" />
  <Boolean key="test17_autobuild_available" value="True" />
  <Int32 key="StartedLevel test17" value="1" />
  <Int32 key="test17_contraption" value="1" />
  <Int32 key="test17_challenge_0" value="2" />
  <Int32 key="test17_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest17" value="1" />
  <Int32 key="exp_LevelComplete2Startest17" value="1" />
  <Int32 key="exp_LevelComplete3Startest17" value="1" />
  <Int32 key="test17_stars" value="3" />
  <String key="Level_37_dessert_placement" value="DessertPlace07:CreamyBun" />
  <Boolean key="Level_37_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_37" value="1" />
  <Int32 key="Level_37_contraption" value="1" />
  <Int32 key="Level_37_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_37" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_37" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_37" value="1" />
  <Int32 key="Level_37_stars" value="3" />
  <String key="test06_dessert_placement" value="" />
  <Boolean key="test06_autobuild_available" value="True" />
  <Int32 key="StartedLevel test06" value="1" />
  <Int32 key="test06_contraption" value="1" />
  <Int32 key="test06_challenge_0" value="2" />
  <Int32 key="test06_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest06" value="1" />
  <Int32 key="exp_LevelComplete2Startest06" value="1" />
  <Int32 key="exp_LevelComplete3Startest06" value="1" />
  <Int32 key="test06_stars" value="3" />
  <String key="Level_38_dessert_placement" value="DessertPlace01:Cupcake;DessertPlace05:IcecreamBalls" />
  <Boolean key="Level_38_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_38" value="1" />
  <Int32 key="Level_38_contraption" value="1" />
  <Int32 key="Level_38_challenge_0" value="2" />
  <Int32 key="Level_38_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_38" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_38" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_38" value="1" />
  <Int32 key="Level_38_stars" value="3" />
  <String key="Level_39_dessert_placement" value="" />
  <Boolean key="Level_39_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_39" value="1" />
  <Int32 key="Level_39_contraption" value="1" />
  <Int32 key="Level_39_challenge_0" value="2" />
  <Int32 key="Level_39_challenge_1" value="2" />
  <Int32 key="Level_39_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_39" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_39" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_39" value="1" />
  <Int32 key="Level_39_stars" value="3" />
  <String key="Level_40_dessert_placement" value="" />
  <Boolean key="Level_40_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_40" value="1" />
  <Int32 key="Level_40_contraption" value="1" />
  <Int32 key="Level_40_challenge_0" value="2" />
  <Int32 key="Level_40_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_40" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_40" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_40" value="1" />
  <Int32 key="Level_40_stars" value="3" />
  <String key="Level_41_dessert_placement" value="" />
  <Boolean key="Level_41_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_41" value="1" />
  <Int32 key="Level_41_contraption" value="1" />
  <Int32 key="Level_41_challenge_0" value="2" />
  <Int32 key="Level_41_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_41" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_41" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_41" value="1" />
  <Int32 key="Level_41_stars" value="3" />
  <String key="Level_09_dessert_placement" value="" />
  <Boolean key="Level_09_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_09" value="1" />
  <Int32 key="Level_09_contraption" value="1" />
  <Int32 key="Level_09_challenge_0" value="2" />
  <Int32 key="Level_09_challenge_1" value="2" />
  <Int32 key="Level_09_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_09" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_09" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_09" value="1" />
  <Int32 key="Level_09_stars" value="3" />
  <String key="Level_19_dessert_placement" value="DessertPlace01:VanillaCakeSlice" />
  <Boolean key="Level_19_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_19" value="1" />
  <Int32 key="Level_19_contraption" value="1" />
  <Int32 key="Level_19_challenge_0" value="2" />
  <Int32 key="Level_19_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_19" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_19" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_19" value="1" />
  <Int32 key="Level_19_stars" value="3" />
  <String key="test04_dessert_placement" value="DessertPlace01:Cupcake" />
  <Boolean key="test04_autobuild_available" value="True" />
  <Int32 key="StartedLevel test04" value="1" />
  <Int32 key="test04_contraption" value="1" />
  <Int32 key="test04_challenge_0" value="2" />
  <Int32 key="test04_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest04" value="1" />
  <Int32 key="exp_LevelComplete2Startest04" value="1" />
  <Int32 key="exp_LevelComplete3Startest04" value="1" />
  <Int32 key="test04_stars" value="3" />
  <String key="Level_42_dessert_placement" value="" />
  <Boolean key="Level_42_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_42" value="1" />
  <Int32 key="Level_42_contraption" value="1" />
  <Int32 key="Level_42_challenge_0" value="2" />
  <Int32 key="Level_42_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_42" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_42" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_42" value="1" />
  <Int32 key="Level_42_stars" value="3" />
  <String key="Level_44_dessert_placement" value="DessertPlace01:CreamyBun" />
  <Boolean key="Level_44_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_44" value="1" />
  <Int32 key="Level_44_contraption" value="1" />
  <Int32 key="Level_44_challenge_0" value="2" />
  <Int32 key="Level_44_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_44" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_44" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_44" value="1" />
  <Int32 key="Level_44_stars" value="3" />
  <String key="Level_46_dessert_placement" value="DessertPlace03:CreamyBun" />
  <Boolean key="Level_46_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_46" value="1" />
  <Int32 key="Level_46_contraption" value="1" />
  <Int32 key="Level_46_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_46" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_46" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_46" value="1" />
  <Int32 key="Level_46_stars" value="3" />
  <String key="Level_45_dessert_placement" value="DessertPlace06:StrawberryCake" />
  <Boolean key="Level_45_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_45" value="1" />
  <Int32 key="Level_45_contraption" value="1" />
  <Int32 key="Level_45_challenge_0" value="2" />
  <Int32 key="Level_45_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_45" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_45" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_45" value="1" />
  <Int32 key="Level_45_stars" value="3" />
  <String key="Level_47_dessert_placement" value="DessertPlace02:VanillaCakeSlice" />
  <Boolean key="Level_47_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_47" value="1" />
  <Int32 key="Level_47_contraption" value="1" />
  <Int32 key="Level_47_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_47" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_47" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_47" value="1" />
  <Int32 key="Level_47_stars" value="3" />
  <String key="Level_06_dessert_placement" value="" />
  <Boolean key="Level_06_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_06" value="1" />
  <Int32 key="Level_06_contraption" value="1" />
  <Int32 key="Level_06_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_06" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_06" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_06" value="1" />
  <Int32 key="Level_06_stars" value="3" />
  <String key="test07_dessert_placement" value="DessertPlace05:CreamyBun" />
  <Boolean key="test07_autobuild_available" value="True" />
  <Int32 key="StartedLevel test07" value="1" />
  <Int32 key="test07_contraption" value="1" />
  <Int32 key="test07_challenge_0" value="2" />
  <Int32 key="test07_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest07" value="1" />
  <Int32 key="exp_LevelComplete2Startest07" value="1" />
  <Int32 key="exp_LevelComplete3Startest07" value="1" />
  <Int32 key="test07_stars" value="3" />
  <String key="Level_08_dessert_placement" value="" />
  <Boolean key="Level_08_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_08" value="1" />
  <Int32 key="Level_08_contraption" value="1" />
  <Int32 key="Level_08_challenge_0" value="2" />
  <Int32 key="Level_08_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_08" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_08" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_08" value="1" />
  <Int32 key="Level_08_stars" value="3" />
  <String key="test10_dessert_placement" value="DessertPlace05:CreamyBun;DessertPlace02:StrawberryCake" />
  <Boolean key="test10_autobuild_available" value="True" />
  <Int32 key="StartedLevel test10" value="1" />
  <Int32 key="test10_contraption" value="1" />
  <Int32 key="test10_challenge_0" value="2" />
  <Int32 key="test10_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest10" value="1" />
  <Int32 key="exp_LevelComplete2Startest10" value="1" />
  <Int32 key="exp_LevelComplete3Startest10" value="1" />
  <Int32 key="test10_stars" value="3" />
  <String key="test08_dessert_placement" value="" />
  <Boolean key="test08_autobuild_available" value="True" />
  <Int32 key="StartedLevel test08" value="1" />
  <Int32 key="test08_contraption" value="1" />
  <Int32 key="test08_challenge_0" value="2" />
  <Int32 key="test08_challenge_1" value="2" />
  <Int32 key="test08_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest08" value="1" />
  <Int32 key="exp_LevelComplete2Startest08" value="1" />
  <Int32 key="exp_LevelComplete3Startest08" value="1" />
  <Int32 key="test08_stars" value="3" />
  <String key="Level_13_dessert_placement" value="" />
  <Boolean key="Level_13_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_13" value="1" />
  <Int32 key="Level_13_contraption" value="1" />
  <Int32 key="Level_13_challenge_0" value="2" />
  <Int32 key="Level_13_challenge_1" value="2" />
  <Int32 key="Level_13_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_13" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_13" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_13" value="1" />
  <Int32 key="Level_13_stars" value="3" />
  <String key="test27_dessert_placement" value="" />
  <Boolean key="test27_autobuild_available" value="True" />
  <Int32 key="StartedLevel test27" value="1" />
  <Int32 key="test27_contraption" value="1" />
  <Int32 key="test27_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest27" value="1" />
  <Int32 key="exp_LevelComplete2Startest27" value="1" />
  <Int32 key="exp_LevelComplete3Startest27" value="1" />
  <Int32 key="test27_stars" value="3" />
  <String key="Level_10_dessert_placement" value="DessertPlace05:StrawberryCake" />
  <Boolean key="Level_10_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_10" value="1" />
  <Int32 key="Level_10_contraption" value="1" />
  <Int32 key="Level_10_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_10" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_10" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_10" value="1" />
  <Int32 key="Level_10_stars" value="3" />
  <Int32 key="Episode2_End_played" value="1" />
  <Boolean key="FlurryEventSent_Day 1 Retention" value="True" />
  <String key="Level_35_dessert_placement" value="DessertPlace08:StrawberryCake" />
  <Boolean key="Level_35_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_35" value="1" />
  <Int32 key="Level_35_contraption" value="1" />
  <Int32 key="Level_35_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_35" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_35" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_35" value="1" />
  <Int32 key="Level_35_stars" value="3" />
  <String key="Level_34_dessert_placement" value="" />
  <Boolean key="Level_34_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_34" value="1" />
  <Int32 key="Level_34_contraption" value="1" />
  <Int32 key="Level_34_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_34" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_34" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_34" value="1" />
  <Int32 key="Level_34_stars" value="3" />
  <Boolean key="Level_36_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_36" value="1" />
  <Int32 key="Level_36_contraption" value="1" />
  <Int32 key="Level_36_challenge_0" value="2" />
  <Int32 key="Level_36_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_36" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_36" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_36" value="1" />
  <Int32 key="Level_36_stars" value="3" />
  <String key="test18_dessert_placement" value="" />
  <Boolean key="test18_autobuild_available" value="True" />
  <Int32 key="StartedLevel test18" value="1" />
  <Int32 key="test18_contraption" value="1" />
  <Int32 key="test18_challenge_0" value="2" />
  <Int32 key="test18_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest18" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest18" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest18" value="1" />
  <Int32 key="test18_stars" value="3" />
  <String key="test50_dessert_placement" value="DessertPlace06:CreamyBun;DessertPlace05:CreamyBun" />
  <Boolean key="test50_autobuild_available" value="True" />
  <Int32 key="StartedLevel test50" value="1" />
  <Int32 key="test50_contraption" value="1" />
  <Int32 key="test50_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest50" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest50" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest50" value="1" />
  <Int32 key="test50_stars" value="3" />
  <String key="Level_48_dessert_placement" value="DessertPlace24:CreamyBun;DessertPlace30:CreamyBun;DessertPlace08:Cupcake" />
  <Boolean key="Level_48_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_48" value="1" />
  <Int32 key="Level_48_contraption" value="1" />
  <Int32 key="Level_48_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1StarLevel_48" value="1" />
  <Int32 key="exp_JokerLevelComplete2StarLevel_48" value="1" />
  <Int32 key="exp_JokerLevelComplete3StarLevel_48" value="1" />
  <Int32 key="Level_48_stars" value="3" />
  <String key="test12_dessert_placement" value="" />
  <Boolean key="test12_autobuild_available" value="True" />
  <Int32 key="StartedLevel test12" value="1" />
  <Int32 key="test12_contraption" value="1" />
  <Int32 key="test12_challenge_0" value="2" />
  <Int32 key="test12_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest12" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest12" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest12" value="1" />
  <Int32 key="test12_stars" value="3" />
  <String key="test09_dessert_placement" value="DessertPlace02:StrawberryCake" />
  <Boolean key="test09_autobuild_available" value="True" />
  <Int32 key="StartedLevel test09" value="1" />
  <Int32 key="test09_contraption" value="1" />
  <Int32 key="test09_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest09" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest09" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest09" value="1" />
  <Int32 key="test09_stars" value="3" />
  <String key="test16_dessert_placement" value="DessertPlace25:Cupcake;DessertPlace30:StrawberryCake;DessertPlace29:Cupcake" />
  <Boolean key="test16_autobuild_available" value="True" />
  <Int32 key="StartedLevel test16" value="1" />
  <Int32 key="test16_contraption" value="1" />
  <Int32 key="test16_challenge_0" value="2" />
  <Int32 key="test16_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest16" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest16" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest16" value="1" />
  <Int32 key="test16_stars" value="3" />
  <Boolean key="SecretPumpkin" value="True" />
  <Boolean key="Part_Pumpkin_02_SET" value="True" />
  <Boolean key="Part_Pumpkin_02_SET_isNew" value="False" />
  <Boolean key="Part_Pumpkin_02_SET_isUsed" value="True" />
  <Boolean key="IAPRestored" value="True" />
  <Int32 key="Episode3_Start_played" value="1" />
  <String key="Level_43_dessert_placement" value="" />
  <Boolean key="Level_43_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_43" value="1" />
  <Int32 key="Level_43_contraption" value="1" />
  <Int32 key="Level_43_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_43" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_43" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_43" value="1" />
  <Int32 key="Level_43_stars" value="3" />
  <String key="Level_51_dessert_placement" value="DessertPlace02:Cupcake" />
  <Boolean key="Level_51_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_51" value="1" />
  <Int32 key="Level_51_contraption" value="1" />
  <Int32 key="Level_51_challenge_0" value="2" />
  <Int32 key="Level_51_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_51" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_51" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_51" value="1" />
  <Int32 key="Level_51_stars" value="3" />
  <String key="scenario_11_dessert_placement" value="DessertPlace09:IcecreamBalls" />
  <Boolean key="scenario_11_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_11" value="1" />
  <Int32 key="scenario_11_contraption" value="1" />
  <Int32 key="scenario_11_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_11" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_11" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_11" value="1" />
  <Int32 key="scenario_11_stars" value="3" />
  <String key="test20_dessert_placement" value="" />
  <Boolean key="test20_autobuild_available" value="True" />
  <Int32 key="StartedLevel test20" value="1" />
  <Int32 key="test20_contraption" value="1" />
  <Int32 key="test20_challenge_0" value="2" />
  <Int32 key="test20_challenge_1" value="2" />
  <Int32 key="test20_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest20" value="1" />
  <Int32 key="exp_LevelComplete2Startest20" value="1" />
  <Int32 key="exp_LevelComplete3Startest20" value="1" />
  <Int32 key="test20_stars" value="3" />
  <String key="scenario_18_dessert_placement" value="" />
  <Boolean key="scenario_18_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_18" value="1" />
  <Int32 key="scenario_18_contraption" value="1" />
  <Int32 key="scenario_18_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_18" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_18" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_18" value="1" />
  <Int32 key="scenario_18_stars" value="3" />
  <String key="Level_53_dessert_placement" value="DessertPlace04:CreamyBun;DessertPlace08:VanillaCakeSlice" />
  <Boolean key="Level_53_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_53" value="1" />
  <Int32 key="Level_53_contraption" value="1" />
  <Int32 key="Level_53_challenge_0" value="2" />
  <Int32 key="Level_53_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_53" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_53" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_53" value="1" />
  <Int32 key="Level_53_stars" value="3" />
  <String key="Level_52_dessert_placement" value="" />
  <Boolean key="Level_52_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_52" value="1" />
  <Int32 key="Level_52_contraption" value="1" />
  <Int32 key="Level_52_challenge_0" value="2" />
  <Int32 key="Level_52_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_52" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_52" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_52" value="1" />
  <Int32 key="Level_52_stars" value="3" />
  <String key="Level_54_dessert_placement" value="" />
  <Boolean key="Level_54_autobuild_available" value="True" />
  <Int32 key="StartedLevel Level_54" value="1" />
  <Int32 key="Level_54_contraption" value="1" />
  <Int32 key="Level_54_challenge_0" value="2" />
  <Int32 key="Level_54_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_54" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_54" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_54" value="1" />
  <Int32 key="Level_54_stars" value="3" />
  <String key="scenario_03_dessert_placement" value="DessertPlace03:IcecreamBalls;DessertPlace07:Cupcake;DessertPlace02:IcecreamBalls" />
  <Boolean key="scenario_03_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_03" value="1" />
  <Int32 key="scenario_03_contraption" value="1" />
  <Int32 key="scenario_03_challenge_0" value="2" />
  <Int32 key="scenario_03_challenge_1" value="2" />
  <Int32 key="scenario_03_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_03" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_03" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_03" value="1" />
  <Int32 key="scenario_03_stars" value="3" />
  <String key="test52_dessert_placement" value="" />
  <Boolean key="test52_autobuild_available" value="True" />
  <Int32 key="StartedLevel test52" value="1" />
  <Int32 key="test52_contraption" value="1" />
  <Int32 key="test52_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Startest52" value="1" />
  <Int32 key="exp_LevelComplete2Startest52" value="1" />
  <Int32 key="exp_LevelComplete3Startest52" value="1" />
  <Int32 key="test52_stars" value="3" />
  <String key="scenario_20_dessert_placement" value="" />
  <Boolean key="scenario_20_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_20" value="1" />
  <Int32 key="scenario_20_contraption" value="1" />
  <Int32 key="scenario_20_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_20" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_20" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_20" value="1" />
  <Int32 key="scenario_20_stars" value="3" />
  <String key="test54_dessert_placement" value="" />
  <Boolean key="test54_autobuild_available" value="True" />
  <Int32 key="StartedLevel test54" value="1" />
  <Int32 key="test54_contraption" value="1" />
  <Int32 key="test54_challenge_0" value="2" />
  <Int32 key="test54_challenge_1" value="2" />
  <Int32 key="test54_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest54" value="1" />
  <Int32 key="exp_LevelComplete2Startest54" value="1" />
  <Int32 key="exp_LevelComplete3Startest54" value="1" />
  <Int32 key="test54_stars" value="3" />
  <String key="scenario_22_dessert_placement" value="" />
  <Boolean key="scenario_22_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_22" value="1" />
  <Int32 key="scenario_22_contraption" value="1" />
  <Int32 key="scenario_22_challenge_0" value="2" />
  <Int32 key="scenario_22_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_22" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_22" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_22" value="1" />
  <Int32 key="scenario_22_stars" value="3" />
  <String key="scenario_16_dessert_placement" value="" />
  <Boolean key="scenario_16_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_16" value="1" />
  <Int32 key="scenario_16_contraption" value="1" />
  <Int32 key="scenario_16_challenge_0" value="2" />
  <Int32 key="scenario_16_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_16" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_16" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_16" value="1" />
  <Int32 key="scenario_16_stars" value="3" />
  <String key="scenario_12_dessert_placement" value="" />
  <Boolean key="scenario_12_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_12" value="1" />
  <Int32 key="scenario_12_contraption" value="1" />
  <Int32 key="scenario_12_challenge_0" value="2" />
  <Int32 key="scenario_12_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_12" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_12" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_12" value="1" />
  <Int32 key="scenario_12_stars" value="3" />
  <String key="scenario_14_dessert_placement" value="DessertPlace02:StrawberryCake" />
  <Boolean key="scenario_14_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_14" value="1" />
  <Int32 key="scenario_14_contraption" value="1" />
  <Int32 key="scenario_14_challenge_0" value="2" />
  <Int32 key="scenario_14_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_14" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_14" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_14" value="1" />
  <Int32 key="scenario_14_stars" value="3" />
  <String key="scenario_32_dessert_placement" value="" />
  <Boolean key="scenario_32_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_32" value="1" />
  <Int32 key="scenario_32_contraption" value="1" />
  <Int32 key="scenario_32_challenge_0" value="2" />
  <Int32 key="scenario_32_challenge_1" value="2" />
  <Int32 key="scenario_32_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_32" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_32" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_32" value="1" />
  <Int32 key="scenario_32_stars" value="3" />
  <String key="scenario_33_dessert_placement" value="" />
  <Boolean key="scenario_33_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_33" value="1" />
  <Int32 key="scenario_33_contraption" value="1" />
  <Int32 key="scenario_33_challenge_0" value="2" />
  <Int32 key="scenario_33_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_33" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_33" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_33" value="1" />
  <Int32 key="scenario_33_stars" value="3" />
  <String key="scenario_40_dessert_placement" value="" />
  <Boolean key="scenario_40_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_40" value="1" />
  <Int32 key="scenario_40_contraption" value="1" />
  <Int32 key="scenario_40_challenge_0" value="2" />
  <Int32 key="scenario_40_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_40" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_40" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_40" value="1" />
  <Int32 key="scenario_40_stars" value="3" />
  <String key="track_07_dessert_placement" value="" />
  <Boolean key="track_07_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_07" value="1" />
  <Int32 key="track_07_contraption" value="1" />
  <Int32 key="track_07_challenge_0" value="2" />
  <Int32 key="track_07_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_07" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_07" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_07" value="1" />
  <Int32 key="track_07_stars" value="3" />
  <String key="scenario_54_dessert_placement" value="" />
  <Boolean key="scenario_54_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_54" value="1" />
  <Int32 key="scenario_54_contraption" value="1" />
  <Int32 key="scenario_54_challenge_0" value="2" />
  <Int32 key="scenario_54_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_54" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_54" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_54" value="1" />
  <Int32 key="scenario_54_stars" value="3" />
  <String key="scenario_53_dessert_placement" value="" />
  <Boolean key="scenario_53_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_53" value="1" />
  <Int32 key="scenario_53_contraption" value="1" />
  <Int32 key="scenario_53_challenge_0" value="2" />
  <Int32 key="scenario_53_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_53" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_53" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_53" value="1" />
  <Int32 key="scenario_53_stars" value="3" />
  <String key="scenario_52_dessert_placement" value="DessertPlace01:Cupcake" />
  <Boolean key="scenario_52_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_52" value="1" />
  <Int32 key="scenario_52_contraption" value="1" />
  <Int32 key="scenario_52_challenge_0" value="2" />
  <Int32 key="scenario_52_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_52" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_52" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_52" value="1" />
  <Int32 key="scenario_52_stars" value="3" />
  <String key="scenario_51_dessert_placement" value="" />
  <Boolean key="scenario_51_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_51" value="1" />
  <Int32 key="scenario_51_contraption" value="1" />
  <Int32 key="scenario_51_challenge_0" value="2" />
  <Int32 key="scenario_51_challenge_1" value="2" />
  <Int32 key="scenario_51_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_51" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_51" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_51" value="1" />
  <Int32 key="scenario_51_stars" value="3" />
  <String key="scenario_35_dessert_placement" value="DessertPlace13:Cupcake" />
  <Boolean key="scenario_35_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_35" value="1" />
  <Int32 key="scenario_35_contraption" value="1" />
  <Int32 key="scenario_35_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_35" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_35" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_35" value="1" />
  <Int32 key="scenario_35_stars" value="3" />
  <String key="scenario_36_dessert_placement" value="DessertPlace08:VanillaCakeSlice" />
  <Int32 key="test49_challenge_2" value="2" />
  <Int32 key="scenario_52_challenge_2" value="2" />
  <Boolean key="SECRET_DISCOVERED_test02" value="True" />
  <String key="test02_dessert_placement" value="DessertPlace08:IcecreamBalls" />
  <Boolean key="scenario_36_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_36" value="1" />
  <Int32 key="scenario_36_contraption" value="1" />
  <Int32 key="scenario_36_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_36" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_36" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_36" value="1" />
  <Int32 key="scenario_36_stars" value="3" />
  <String key="scenario_39_dessert_placement" value="" />
  <Boolean key="scenario_39_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_39" value="1" />
  <Int32 key="scenario_39_contraption" value="1" />
  <Int32 key="scenario_39_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_39" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_39" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_39" value="1" />
  <Int32 key="scenario_39_stars" value="3" />
  <String key="scenario_56_dessert_placement" value="" />
  <Boolean key="scenario_56_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_56" value="1" />
  <Int32 key="scenario_56_contraption" value="1" />
  <Int32 key="scenario_56_challenge_0" value="2" />
  <Int32 key="scenario_56_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_56" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_56" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_56" value="1" />
  <Int32 key="scenario_56_stars" value="3" />
  <String key="scenario_29_dessert_placement" value="DessertPlace06:CreamyBun" />
  <Boolean key="scenario_29_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_29" value="1" />
  <Int32 key="scenario_29_contraption" value="1" />
  <Int32 key="scenario_29_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_29" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_29" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_29" value="1" />
  <Int32 key="scenario_29_stars" value="3" />
  <String key="scenario_27_dessert_placement" value="" />
  <Boolean key="scenario_27_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_27" value="1" />
  <Int32 key="scenario_27_contraption" value="1" />
  <Int32 key="scenario_27_challenge_0" value="2" />
  <Int32 key="scenario_27_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_27" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_27" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_27" value="1" />
  <Int32 key="scenario_27_stars" value="3" />
  <String key="scenario_28_dessert_placement" value="" />
  <Boolean key="scenario_28_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_28" value="1" />
  <Int32 key="scenario_28_contraption" value="1" />
  <Int32 key="scenario_28_challenge_0" value="2" />
  <Int32 key="scenario_28_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_28" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_28" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_28" value="1" />
  <Int32 key="scenario_28_stars" value="3" />
  <String key="scenario_25_dessert_placement" value="DessertPlace06:CreamyBun" />
  <Boolean key="scenario_25_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_25" value="1" />
  <Int32 key="scenario_25_contraption" value="1" />
  <Int32 key="scenario_25_challenge_0" value="2" />
  <Int32 key="scenario_25_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_25" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_25" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_25" value="1" />
  <Int32 key="scenario_25_stars" value="3" />
  <String key="scenario_38_dessert_placement" value="" />
  <Boolean key="scenario_38_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_38" value="1" />
  <Int32 key="scenario_38_contraption" value="1" />
  <Int32 key="scenario_38_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_38" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_38" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_38" value="1" />
  <Int32 key="scenario_38_stars" value="3" />
  <String key="scenario_41_dessert_placement" value="DessertPlace06:CreamyBun" />
  <Boolean key="scenario_41_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_41" value="1" />
  <Int32 key="scenario_41_contraption" value="1" />
  <Int32 key="scenario_41_challenge_0" value="2" />
  <Int32 key="scenario_41_challenge_1" value="2" />
  <Int32 key="scenario_41_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_41" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_41" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_41" value="1" />
  <Int32 key="scenario_41_stars" value="3" />
  <String key="scenario_42_dessert_placement" value="" />
  <Boolean key="scenario_42_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_42" value="1" />
  <Int32 key="scenario_42_contraption" value="1" />
  <Int32 key="scenario_42_challenge_0" value="2" />
  <Int32 key="scenario_42_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_42" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_42" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_42" value="1" />
  <Int32 key="scenario_42_stars" value="3" />
  <String key="scenario_50_dessert_placement" value="DessertPlace18:VanillaCakeSlice;DessertPlace17:VanillaCakeSlice;DessertPlace16:Cupcake;DessertPlace02:StrawberryCake" />
  <Boolean key="scenario_50_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_50" value="1" />
  <Int32 key="scenario_50_contraption" value="1" />
  <Int32 key="scenario_50_challenge_0" value="2" />
  <Int32 key="scenario_50_challenge_1" value="2" />
  <Int32 key="scenario_50_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_50" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_50" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_50" value="1" />
  <Int32 key="scenario_50_stars" value="3" />
  <Int32 key="Episode3_End_played" value="1" />
  <String key="test15_dessert_placement" value="" />
  <Boolean key="test15_autobuild_available" value="True" />
  <Int32 key="StartedLevel test15" value="1" />
  <Int32 key="test15_contraption" value="1" />
  <Int32 key="test15_challenge_0" value="2" />
  <Int32 key="test15_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest15" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest15" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest15" value="1" />
  <Int32 key="test15_stars" value="3" />
  <String key="test59_dessert_placement" value="" />
  <Boolean key="test59_autobuild_available" value="True" />
  <Int32 key="StartedLevel test59" value="1" />
  <Int32 key="test59_contraption" value="1" />
  <Int32 key="test59_challenge_0" value="2" />
  <Int32 key="test59_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest59" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest59" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest59" value="1" />
  <Int32 key="test59_stars" value="3" />
  <String key="test53_dessert_placement" value="" />
  <Boolean key="test53_autobuild_available" value="True" />
  <Int32 key="StartedLevel test53" value="1" />
  <Int32 key="test53_contraption" value="1" />
  <Int32 key="test53_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startest53" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startest53" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startest53" value="1" />
  <Int32 key="test53_stars" value="3" />
  <String key="scenario_15_dessert_placement" value="DessertPlace06:Cupcake" />
  <Boolean key="scenario_15_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_15" value="1" />
  <Int32 key="scenario_15_contraption" value="1" />
  <Int32 key="scenario_15_challenge_0" value="2" />
  <Int32 key="scenario_15_challenge_1" value="2" />
  <Int32 key="scenario_15_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_15" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_15" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_15" value="1" />
  <Int32 key="scenario_15_stars" value="3" />
  <String key="track_05_dessert_placement" value="DessertPlace09:IcecreamBalls" />
  <Boolean key="track_05_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_05" value="1" />
  <Int32 key="track_05_contraption" value="1" />
  <Int32 key="track_05_challenge_0" value="2" />
  <Int32 key="track_05_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startrack_05" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startrack_05" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startrack_05" value="1" />
  <Int32 key="track_05_stars" value="3" />
  <String key="scenario_49_dessert_placement" value="DessertPlace08:Cupcake;DessertPlace09:StrawberryCake" />
  <Boolean key="scenario_49_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_49" value="1" />
  <Int32 key="scenario_49_contraption" value="1" />
  <Int32 key="scenario_49_challenge_0" value="2" />
  <Int32 key="scenario_49_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_49" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_49" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_49" value="1" />
  <Int32 key="scenario_49_stars" value="3" />
  <String key="track_03_dessert_placement" value="DessertPlace04:StrawberryCake;DessertPlace01:VanillaCakeSlice" />
  <Boolean key="track_03_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_03" value="1" />
  <Int32 key="track_03_contraption" value="1" />
  <Int32 key="track_03_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startrack_03" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startrack_03" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startrack_03" value="1" />
  <Int32 key="track_03_stars" value="3" />
  <String key="scenario_30_dessert_placement" value="" />
  <Boolean key="scenario_30_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_30" value="1" />
  <Int32 key="scenario_30_contraption" value="1" />
  <Int32 key="scenario_30_challenge_0" value="2" />
  <Int32 key="scenario_30_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_30" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_30" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_30" value="1" />
  <Int32 key="scenario_30_stars" value="3" />
  <String key="track_06_dessert_placement" value="" />
  <Boolean key="track_06_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_06" value="1" />
  <Int32 key="track_06_contraption" value="1" />
  <Int32 key="track_06_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Startrack_06" value="1" />
  <Int32 key="exp_JokerLevelComplete2Startrack_06" value="1" />
  <Int32 key="exp_JokerLevelComplete3Startrack_06" value="1" />
  <Int32 key="track_06_stars" value="3" />
  <Int32 key="Episode5_Start_played" value="1" />
  <String key="scenario_55_dessert_placement" value="" />
  <Boolean key="scenario_55_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_55" value="1" />
  <Int32 key="scenario_55_contraption" value="1" />
  <Int32 key="scenario_55_challenge_0" value="2" />
  <Int32 key="scenario_55_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_55" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_55" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_55" value="1" />
  <Int32 key="scenario_55_stars" value="3" />
  <String key="scenario_45_dessert_placement" value="DessertPlace24:CreamyBun" />
  <Boolean key="scenario_45_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_45" value="1" />
  <Int32 key="scenario_45_contraption" value="1" />
  <Int32 key="scenario_45_challenge_0" value="2" />
  <Int32 key="scenario_45_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_45" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_45" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_45" value="1" />
  <Int32 key="scenario_45_stars" value="3" />
  <String key="scenario_26_dessert_placement" value="DessertPlace26:VanillaCakeSlice" />
  <Boolean key="scenario_26_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_26" value="1" />
  <Int32 key="scenario_26_contraption" value="1" />
  <Int32 key="scenario_26_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_26" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_26" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_26" value="1" />
  <Int32 key="scenario_26_stars" value="3" />
  <String key="scenario_44_dessert_placement" value="" />
  <Boolean key="scenario_44_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_44" value="1" />
  <Int32 key="scenario_44_contraption" value="1" />
  <Int32 key="scenario_44_challenge_0" value="2" />
  <Int32 key="scenario_44_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_44" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_44" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_44" value="1" />
  <Int32 key="scenario_44_stars" value="3" />
  <String key="scenario_24_dessert_placement" value="" />
  <Boolean key="scenario_24_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_24" value="1" />
  <Int32 key="scenario_24_contraption" value="1" />
  <Int32 key="scenario_24_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_24" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_24" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_24" value="1" />
  <Int32 key="scenario_24_stars" value="3" />
  <String key="track_04_dessert_placement" value="" />
  <Boolean key="track_04_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_04" value="1" />
  <Int32 key="track_04_contraption" value="1" />
  <Int32 key="track_04_challenge_0" value="2" />
  <Int32 key="track_04_challenge_1" value="2" />
  <Int32 key="track_04_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_04" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_04" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_04" value="1" />
  <Int32 key="track_04_stars" value="3" />
  <String key="scenario_37_dessert_placement" value="" />
  <Boolean key="scenario_37_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_37" value="1" />
  <Int32 key="scenario_37_contraption" value="1" />
  <Int32 key="scenario_37_challenge_0" value="2" />
  <Int32 key="scenario_37_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_37" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_37" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_37" value="1" />
  <Int32 key="scenario_37_stars" value="3" />
  <String key="scenario_21_dessert_placement" value="DessertPlace29:Cupcake;DessertPlace28:IcecreamBalls" />
  <Boolean key="scenario_21_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_21" value="1" />
  <Int32 key="scenario_21_contraption" value="1" />
  <Int32 key="scenario_21_challenge_0" value="2" />
  <Int32 key="scenario_21_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_21" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_21" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_21" value="1" />
  <Int32 key="scenario_21_stars" value="3" />
  <String key="scenario_02_dessert_placement" value="DessertPlace20:IcecreamBalls;DessertPlace01:IcecreamBalls;DessertPlace27:VanillaCakeSlice" />
  <Boolean key="scenario_02_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_02" value="1" />
  <Int32 key="scenario_02_contraption" value="1" />
  <Int32 key="scenario_02_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_02" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_02" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_02" value="1" />
  <Int32 key="scenario_02_stars" value="3" />
  <String key="test55_dessert_placement" value="DessertPlace11:IcecreamBalls;DessertPlace21:CreamyBun" />
  <Boolean key="test55_autobuild_available" value="True" />
  <Int32 key="StartedLevel test55" value="1" />
  <Int32 key="test55_contraption" value="1" />
  <Int32 key="test55_challenge_0" value="2" />
  <Int32 key="test55_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Startest55" value="1" />
  <Int32 key="exp_LevelComplete2Startest55" value="1" />
  <Int32 key="exp_LevelComplete3Startest55" value="1" />
  <Int32 key="test55_stars" value="3" />
  <String key="test57_dessert_placement" value="" />
  <Boolean key="test57_autobuild_available" value="True" />
  <Int32 key="StartedLevel test57" value="1" />
  <Int32 key="test57_contraption" value="1" />
  <Int32 key="test57_challenge_0" value="2" />
  <Int32 key="test57_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest57" value="1" />
  <Int32 key="exp_LevelComplete2Startest57" value="1" />
  <Int32 key="exp_LevelComplete3Startest57" value="1" />
  <Int32 key="test57_stars" value="3" />
  <String key="scenario_31_dessert_placement" value="" />
  <Boolean key="scenario_31_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_31" value="1" />
  <Int32 key="scenario_31_contraption" value="1" />
  <Int32 key="scenario_31_challenge_0" value="2" />
  <Int32 key="scenario_31_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_31" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_31" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_31" value="1" />
  <Int32 key="scenario_31_stars" value="3" />
  <Int32 key="Episode5_Mid_played" value="1" />
  <String key="test30_dessert_placement" value="" />
  <Boolean key="test30_autobuild_available" value="True" />
  <Int32 key="StartedLevel test30" value="1" />
  <Int32 key="test30_contraption" value="1" />
  <Int32 key="test30_challenge_0" value="2" />
  <Int32 key="test30_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startest30" value="1" />
  <Int32 key="exp_LevelComplete2Startest30" value="1" />
  <Int32 key="exp_LevelComplete3Startest30" value="1" />
  <Int32 key="test30_stars" value="3" />
  <String key="track_13_dessert_placement" value="" />
  <Boolean key="track_13_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_13" value="1" />
  <Int32 key="track_13_contraption" value="1" />
  <Int32 key="track_13_challenge_0" value="2" />
  <Int32 key="track_13_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_13" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_13" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_13" value="1" />
  <Int32 key="track_13_stars" value="3" />
  <String key="scenario_83_dessert_placement" value="DessertPlace03:CreamyBun;DessertPlace27:CreamyBun" />
  <Boolean key="scenario_83_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_83" value="1" />
  <Int32 key="scenario_83_contraption" value="1" />
  <Int32 key="scenario_83_challenge_0" value="2" />
  <Int32 key="scenario_83_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_83" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_83" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_83" value="1" />
  <Int32 key="scenario_83_stars" value="3" />
  <String key="scenario_05_dessert_placement" value="DessertPlace07:CreamyBun" />
  <Boolean key="scenario_05_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_05" value="1" />
  <Int32 key="scenario_05_contraption" value="1" />
  <Int32 key="scenario_05_challenge_0" value="2" />
  <Int32 key="scenario_05_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_05" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_05" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_05" value="1" />
  <Int32 key="scenario_05_stars" value="3" />
  <String key="scenario_100_dessert_placement" value="DessertPlace17:Cupcake;DessertPlace04:CreamyBun;DessertPlace10:StrawberryCake" />
  <Boolean key="scenario_100_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_100" value="1" />
  <Int32 key="scenario_100_contraption" value="1" />
  <Int32 key="scenario_100_challenge_0" value="2" />
  <Int32 key="scenario_100_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_100" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_100" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_100" value="1" />
  <Int32 key="scenario_100_stars" value="3" />
  <String key="scenario_09_dessert_placement" value="DessertPlace20:IcecreamBalls;DessertPlace19:Cupcake" />
  <Boolean key="scenario_09_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_09" value="1" />
  <Int32 key="scenario_09_contraption" value="1" />
  <Int32 key="scenario_09_challenge_0" value="2" />
  <Int32 key="scenario_09_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_09" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_09" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_09" value="1" />
  <Int32 key="scenario_09_stars" value="3" />
  <String key="scenario_78_dessert_placement" value="DessertPlace11:CreamyBun" />
  <Boolean key="scenario_78_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_78" value="1" />
  <Int32 key="scenario_78_contraption" value="1" />
  <Int32 key="scenario_78_challenge_0" value="2" />
  <Int32 key="scenario_78_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_78" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_78" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_78" value="1" />
  <Int32 key="scenario_78_stars" value="3" />
  <String key="scenario_13_dessert_placement" value="DessertPlace06:VanillaCakeSlice" />
  <Boolean key="scenario_13_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_13" value="1" />
  <Int32 key="scenario_13_contraption" value="1" />
  <Int32 key="scenario_13_challenge_0" value="2" />
  <Int32 key="scenario_13_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_13" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_13" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_13" value="1" />
  <Int32 key="scenario_13_stars" value="3" />
  <String key="scenario_95_dessert_placement" value="DessertPlace06:VanillaCakeSlice;DessertPlace04:Cupcake" />
  <Boolean key="scenario_95_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_95" value="1" />
  <Int32 key="scenario_95_contraption" value="1" />
  <Int32 key="scenario_95_challenge_0" value="2" />
  <Int32 key="scenario_95_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_95" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_95" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_95" value="1" />
  <Int32 key="scenario_95_stars" value="3" />
  <String key="scenario_96_dessert_placement" value="DessertPlace15:StrawberryCake;DessertPlace14:IcecreamBalls;DessertPlace01:VanillaCakeSlice" />
  <Boolean key="scenario_96_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_96" value="1" />
  <Int32 key="scenario_96_contraption" value="1" />
  <Int32 key="scenario_96_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_96" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_96" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_96" value="1" />
  <Int32 key="scenario_96_stars" value="3" />
  <String key="scenario_98_dessert_placement" value="" />
  <Boolean key="scenario_98_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_98" value="1" />
  <Int32 key="scenario_98_contraption" value="1" />
  <Int32 key="scenario_98_challenge_0" value="2" />
  <Int32 key="scenario_98_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starscenario_98" value="1" />
  <Int32 key="exp_LevelComplete2Starscenario_98" value="1" />
  <Int32 key="exp_LevelComplete3Starscenario_98" value="1" />
  <Int32 key="scenario_98_stars" value="3" />
  <String key="track_30_dessert_placement" value="" />
  <Boolean key="track_30_autobuild_available" value="True" />
  <Int32 key="StartedLevel track_30" value="1" />
  <Int32 key="track_30_contraption" value="1" />
  <Int32 key="track_30_challenge_0" value="2" />
  <Int32 key="track_30_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Startrack_30" value="1" />
  <Int32 key="exp_LevelComplete2Startrack_30" value="1" />
  <Int32 key="exp_LevelComplete3Startrack_30" value="1" />
  <Int32 key="track_30_stars" value="3" />
  <Int32 key="Episode5_End_played" value="1" />
  <String key="scenario_46_dessert_placement" value="" />
  <Boolean key="scenario_46_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_46" value="1" />
  <Int32 key="scenario_46_contraption" value="1" />
  <Int32 key="scenario_46_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_46" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_46" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_46" value="1" />
  <Int32 key="scenario_46_stars" value="3" />
  <String key="scenario_97_dessert_placement" value="" />
  <Boolean key="scenario_97_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_97" value="1" />
  <Int32 key="scenario_97_contraption" value="1" />
  <Int32 key="scenario_97_challenge_0" value="2" />
  <Int32 key="scenario_97_challenge_1" value="2" />
  <Int32 key="scenario_97_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_97" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_97" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_97" value="1" />
  <Int32 key="scenario_97_stars" value="3" />
  <String key="scenario_10_dessert_placement" value="DessertPlace12:Cupcake" />
  <Boolean key="scenario_10_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_10" value="1" />
  <Int32 key="scenario_10_contraption" value="1" />
  <Int32 key="scenario_10_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_10" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_10" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_10" value="1" />
  <Int32 key="scenario_10_stars" value="3" />
  <String key="scenario_08_dessert_placement" value="" />
  <Boolean key="scenario_08_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_08" value="1" />
  <Int32 key="scenario_08_contraption" value="1" />
  <Int32 key="scenario_08_challenge_0" value="2" />
  <Int32 key="scenario_08_challenge_1" value="2" />
  <Int32 key="scenario_08_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_08" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_08" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_08" value="1" />
  <Int32 key="scenario_08_stars" value="3" />
  <String key="scenario_06_dessert_placement" value="" />
  <Boolean key="scenario_06_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_06" value="1" />
  <Int32 key="scenario_06_contraption" value="1" />
  <Int32 key="scenario_06_challenge_0" value="2" />
  <Int32 key="scenario_06_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_06" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_06" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_06" value="1" />
  <Int32 key="scenario_06_stars" value="3" />
  <String key="scenario_99_dessert_placement" value="DessertPlace11:Cupcake;DessertPlace25:VanillaCakeSlice" />
  <Boolean key="scenario_99_autobuild_available" value="True" />
  <Int32 key="StartedLevel scenario_99" value="1" />
  <Int32 key="scenario_99_contraption" value="1" />
  <Int32 key="scenario_99_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starscenario_99" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starscenario_99" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starscenario_99" value="1" />
  <Int32 key="scenario_99_stars" value="3" />
  <Int32 key="Episode6_Start_played" value="1" />
  <String key="episode_6_level_1_dessert_placement" value="" />
  <Boolean key="episode_6_level_1_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_1" value="1" />
  <Int32 key="episode_6_level_1_contraption" value="1" />
  <Int32 key="episode_6_level_1_challenge_0" value="2" />
  <Int32 key="episode_6_level_1_challenge_1" value="2" />
  <Int32 key="episode_6_level_1_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_1" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_1" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_1" value="1" />
  <Int32 key="episode_6_level_1_stars" value="3" />
  <String key="episode_6_level_2_dessert_placement" value="" />
  <Boolean key="episode_6_level_2_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_2" value="1" />
  <Int32 key="episode_6_level_2_contraption" value="1" />
  <Int32 key="episode_6_level_2_challenge_0" value="2" />
  <Int32 key="episode_6_level_2_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_2" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_2" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_2" value="1" />
  <Int32 key="episode_6_level_2_stars" value="3" />
  <String key="episode_6_level_3_dessert_placement" value="" />
  <Boolean key="episode_6_level_3_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_3" value="1" />
  <Int32 key="episode_6_level_3_contraption" value="1" />
  <Int32 key="episode_6_level_3_challenge_0" value="2" />
  <Int32 key="episode_6_level_3_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_3" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_3" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_3" value="1" />
  <Int32 key="episode_6_level_3_stars" value="3" />
  <String key="episode_6_level_4_dessert_placement" value="" />
  <Boolean key="episode_6_level_4_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_4" value="1" />
  <Int32 key="episode_6_level_4_contraption" value="1" />
  <Int32 key="episode_6_level_4_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_4" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_4" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_4" value="1" />
  <Int32 key="episode_6_level_4_stars" value="3" />
  <String key="episode_6_level_5_dessert_placement" value="" />
  <Boolean key="episode_6_level_5_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_5" value="1" />
  <Int32 key="episode_6_level_5_contraption" value="1" />
  <Int32 key="episode_6_level_5_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_5" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_5" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_5" value="1" />
  <Int32 key="episode_6_level_5_stars" value="3" />
  <String key="episode_6_level_6_dessert_placement" value="" />
  <Boolean key="episode_6_level_6_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_6" value="1" />
  <Int32 key="episode_6_level_6_contraption" value="1" />
  <Int32 key="episode_6_level_6_challenge_0" value="2" />
  <Int32 key="episode_6_level_6_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_6" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_6" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_6" value="1" />
  <Int32 key="episode_6_level_6_stars" value="3" />
  <String key="episode_6_level_7_dessert_placement" value="DessertPlace05:VanillaCakeSlice" />
  <Boolean key="episode_6_level_7_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_7" value="1" />
  <Int32 key="episode_6_level_7_contraption" value="1" />
  <Int32 key="episode_6_level_7_challenge_0" value="2" />
  <Int32 key="episode_6_level_7_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_7" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_7" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_7" value="1" />
  <Int32 key="episode_6_level_7_stars" value="3" />
  <String key="episode_6_level_8_dessert_placement" value="DessertPlace18:StrawberryCake;DessertPlace04:IcecreamBalls;DessertPlace03:IcecreamBalls;DessertPlace15:Cupcake;DessertPlace13:IcecreamBalls" />
  <Boolean key="episode_6_level_8_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_8" value="1" />
  <Int32 key="episode_6_level_8_contraption" value="1" />
  <Int32 key="episode_6_level_8_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_8" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_8" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_8" value="1" />
  <Int32 key="episode_6_level_8_stars" value="3" />
  <String key="episode_6_level_9_dessert_placement" value="DessertPlace05:IcecreamBalls;DessertPlace08:VanillaCakeSlice" />
  <Boolean key="episode_6_level_9_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_9" value="1" />
  <Int32 key="episode_6_level_9_contraption" value="1" />
  <Int32 key="episode_6_level_9_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_9" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_9" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_9" value="1" />
  <Int32 key="episode_6_level_9_stars" value="3" />
  <String key="episode_6_level_10_dessert_placement" value="DessertPlace06:Cupcake;DessertPlace16:Cupcake" />
  <Boolean key="episode_6_level_10_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_10" value="1" />
  <Int32 key="episode_6_level_10_contraption" value="1" />
  <Int32 key="episode_6_level_10_challenge_0" value="2" />
  <Int32 key="episode_6_level_10_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_10" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_10" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_10" value="1" />
  <Int32 key="episode_6_level_10_stars" value="3" />
  <String key="episode_6_level_11_dessert_placement" value="DessertPlace02:Cupcake" />
  <Boolean key="episode_6_level_11_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_11" value="1" />
  <Int32 key="episode_6_level_11_contraption" value="1" />
  <Int32 key="episode_6_level_11_challenge_0" value="2" />
  <Int32 key="episode_6_level_11_challenge_1" value="2" />
  <Int32 key="episode_6_level_11_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_11" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_11" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_11" value="1" />
  <Int32 key="episode_6_level_11_stars" value="3" />
  <String key="episode_6_level_12_dessert_placement" value="DessertPlace04:StrawberryCake;DessertPlace09:VanillaCakeSlice" />
  <Boolean key="episode_6_level_12_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_12" value="1" />
  <Int32 key="episode_6_level_12_contraption" value="1" />
  <Int32 key="episode_6_level_12_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_12" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_12" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_12" value="1" />
  <Int32 key="episode_6_level_12_stars" value="3" />
  <Int32 key="Episode6_Mid_played" value="1" />
  <String key="episode_6_level_13_dessert_placement" value="" />
  <Boolean key="episode_6_level_13_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_13" value="1" />
  <Int32 key="episode_6_level_13_contraption" value="1" />
  <Int32 key="episode_6_level_13_challenge_0" value="2" />
  <Int32 key="episode_6_level_13_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_13" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_13" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_13" value="1" />
  <Int32 key="episode_6_level_13_stars" value="3" />
  <String key="episode_6_level_14_dessert_placement" value="" />
  <Boolean key="episode_6_level_14_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_14" value="1" />
  <Int32 key="episode_6_level_14_contraption" value="1" />
  <Int32 key="episode_6_level_14_challenge_0" value="2" />
  <Int32 key="episode_6_level_14_challenge_1" value="2" />
  <Int32 key="episode_6_level_14_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_14" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_14" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_14" value="1" />
  <Int32 key="episode_6_level_14_stars" value="3" />
  <String key="episode_6_level_15_dessert_placement" value="" />
  <Boolean key="episode_6_level_15_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_15" value="1" />
  <Int32 key="episode_6_level_15_contraption" value="1" />
  <Int32 key="episode_6_level_15_challenge_0" value="2" />
  <Int32 key="episode_6_level_15_challenge_1" value="2" />
  <Int32 key="episode_6_level_15_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_15" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_15" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_15" value="1" />
  <Int32 key="episode_6_level_15_stars" value="3" />
  <String key="episode_6_level_17_dessert_placement" value="DessertPlace04:Cupcake;DessertPlace03:CreamyBun" />
  <Boolean key="episode_6_level_17_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_17" value="1" />
  <Int32 key="episode_6_level_17_contraption" value="1" />
  <Int32 key="episode_6_level_17_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_17" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_17" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_17" value="1" />
  <Int32 key="episode_6_level_17_stars" value="3" />
  <String key="episode_6_level_18_dessert_placement" value="" />
  <Boolean key="episode_6_level_18_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_18" value="1" />
  <Int32 key="episode_6_level_18_contraption" value="1" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_18_statue" value="True" />
  <Int32 key="StatuesFound" value="15" />
  <Int32 key="episode_6_level_18_challenge_0" value="2" />
  <Int32 key="episode_6_level_18_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_18" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_18" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_18" value="1" />
  <Int32 key="episode_6_level_18_stars" value="3" />
  <String key="episode_6_level_19_dessert_placement" value="" />
  <Boolean key="episode_6_level_19_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_19" value="1" />
  <Int32 key="episode_6_level_19_contraption" value="1" />
  <Int32 key="episode_6_level_19_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_19" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_19" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_19" value="1" />
  <Int32 key="episode_6_level_19_stars" value="3" />
  <String key="episode_6_level_20_dessert_placement" value="" />
  <Boolean key="episode_6_level_20_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_20" value="1" />
  <Int32 key="episode_6_level_20_contraption" value="1" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_20_statue" value="True" />
  <Int32 key="episode_6_level_20_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_20" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_20" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_20" value="1" />
  <Int32 key="episode_6_level_20_stars" value="3" />
  <String key="episode_6_level_21_dessert_placement" value="DessertPlace09:VanillaCakeSlice;DessertPlace14:VanillaCakeSlice" />
  <Boolean key="episode_6_level_21_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_21" value="1" />
  <Int32 key="episode_6_level_21_contraption" value="1" />
  <Int32 key="episode_6_level_21_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_21" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_21" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_21" value="1" />
  <Int32 key="episode_6_level_21_stars" value="3" />
  <String key="episode_6_level_22_dessert_placement" value="" />
  <Boolean key="episode_6_level_22_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_22" value="1" />
  <Int32 key="episode_6_level_22_contraption" value="1" />
  <String key="episode_6_level_23_dessert_placement" value="DessertPlace05:IcecreamBalls" />
  <String key="episode_6_level_I_dessert_placement" value="DessertPlace06:Cupcake" />
  <Boolean key="episode_6_level_I_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_I" value="1" />
  <Int32 key="episode_6_level_I_contraption" value="1" />
  <Int32 key="episode_6_level_I_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_I" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_I" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_I" value="1" />
  <Int32 key="episode_6_level_I_stars" value="3" />
  <String key="episode_6_level_II_dessert_placement" value="" />
  <Boolean key="episode_6_level_II_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_II" value="1" />
  <Int32 key="episode_6_level_II_contraption" value="1" />
  <Int32 key="episode_6_level_II_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_II" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_II" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_II" value="1" />
  <Int32 key="episode_6_level_II_stars" value="3" />
  <String key="episode_6_level_III_dessert_placement" value="DessertPlace12:CreamyBun;DessertPlace08:IcecreamBalls;DessertPlace15:VanillaCakeSlice;DessertPlace21:StrawberryCake" />
  <Boolean key="episode_6_level_III_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_III" value="1" />
  <Int32 key="episode_6_level_III_contraption" value="1" />
  <Int32 key="episode_6_level_III_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_III" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_III" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_III" value="1" />
  <Int32 key="episode_6_level_III_stars" value="3" />
  <String key="episode_6_level_IV_dessert_placement" value="DessertPlace01:StrawberryCake" />
  <Boolean key="episode_6_level_IV_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_IV" value="1" />
  <Int32 key="episode_6_level_IV_contraption" value="1" />
  <String key="episode_6_level_V_dessert_placement" value="" />
  <String key="Level_Race_04_dessert_placement" value="" />
  <Int32 key="Level_Race_04_contraption" value="1" />
  <Single key="Level_Race_04_time" value="32.15563" />
  <Int32 key="Level_Race_04_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_04" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_04" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_04" value="1" />
  <Int32 key="Level_Race_04_stars" value="3" />
  <String key="Level_Race_05_dessert_placement" value="DessertPlace23:Cupcake;DessertPlace13:VanillaCakeSlice;DessertPlace11:IcecreamBalls;DessertPlace19:VanillaCakeSlice;DessertPlace02:Cupcake" />
  <Int32 key="StartedLevel Level_Race_05" value="1" />
  <Int32 key="Level_Race_05_contraption" value="1" />
  <Single key="Level_Race_05_time" value="26.48652" />
  <Int32 key="Level_Race_05_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_05" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_05" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_05" value="1" />
  <Int32 key="Level_Race_05_stars" value="3" />
  <String key="Level_Race_06_dessert_placement" value="" />
  <Int32 key="StartedLevel Level_Race_06" value="1" />
  <Int32 key="Level_Race_06_contraption" value="1" />
  <Single key="Level_Race_06_time" value="44.57122" />
  <Int32 key="Level_Race_06_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_06" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_06" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_06" value="1" />
  <Int32 key="Level_Race_06_stars" value="3" />
  <String key="Level_Race_01_dessert_placement" value="DessertPlace21:StrawberryCake;DessertPlace31:StrawberryCake" />
  <Int32 key="Level_Race_01_contraption" value="1" />
  <Single key="Level_Race_01_time" value="83.441" />
  <Int32 key="Level_Race_01_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_01" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_01" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_01" value="1" />
  <Int32 key="Level_Race_01_stars" value="3" />
  <String key="Level_Race_02_dessert_placement" value="DessertPlace43:StrawberryCake;DessertPlace19:Cupcake;DessertPlace17:StrawberryCake;DessertPlace02:VanillaCakeSlice;DessertPlace30:Cupcake" />
  <Int32 key="StartedLevel Level_Race_02" value="1" />
  <Int32 key="Level_Race_02_contraption" value="1" />
  <Single key="Level_Race_02_time" value="66.47647" />
  <Int32 key="Level_Race_02_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_02" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_02" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_02" value="1" />
  <Int32 key="Level_Race_02_stars" value="3" />
  <String key="Level_Race_03_dessert_placement" value="DessertPlace83:StrawberryCake" />
  <Int32 key="StartedLevel Level_Race_03" value="1" />
  <Int32 key="Level_Race_03_contraption" value="1" />
  <Single key="Level_Race_03_time" value="86.92764" />
  <Int32 key="Level_Race_03_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_03" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_03" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_03" value="1" />
  <Int32 key="Level_Race_03_stars" value="3" />
  <String key="Level_Race_07_dessert_placement" value="DessertPlace24:StrawberryCake;DessertPlace74:Cupcake;DessertPlace67:StrawberryCake;DessertPlace42:CreamyBun" />
  <Int32 key="Level_Race_07_contraption" value="1" />
  <Single key="Level_Race_07_time" value="46.03807" />
  <Int32 key="Level_Race_07_challenge_0" value="2" />
  <Int32 key="Level_Race_07_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_07" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_07" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_07" value="1" />
  <Int32 key="Level_Race_07_stars" value="3" />
  <String key="Level_Race_08_dessert_placement" value="DessertPlace10:IcecreamBalls;DessertPlace16:StrawberryCake;DessertPlace07:CreamyBun" />
  <Int32 key="Level_Race_08_contraption" value="1" />
  <Single key="Level_Race_08_time" value="19.79731" />
  <Int32 key="Level_Race_08_challenge_0" value="2" />
  <Int32 key="Level_Race_08_challenge_1" value="2" />
  <Int32 key="Level_Race_08_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1StarLevel_Race_08" value="1" />
  <Int32 key="exp_LevelComplete2StarLevel_Race_08" value="1" />
  <Int32 key="exp_LevelComplete3StarLevel_Race_08" value="1" />
  <Int32 key="Level_Race_08_stars" value="3" />
  <Int32 key="episode_6_level_22_challenge_0" value="2" />
  <Int32 key="episode_6_level_22_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_22" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_22" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_22" value="1" />
  <Int32 key="episode_6_level_22_stars" value="3" />
  <Boolean key="episode_6_level_23_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_23" value="1" />
  <Int32 key="episode_6_level_23_contraption" value="1" />
  <Int32 key="episode_6_level_23_challenge_0" value="2" />
  <Int32 key="episode_6_level_23_challenge_1" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_23" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_23" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_23" value="1" />
  <Int32 key="episode_6_level_23_stars" value="3" />
  <String key="episode_6_level_24_dessert_placement" value="DessertPlace15:Cupcake;DessertPlace02:IcecreamBalls" />
  <Boolean key="episode_6_level_24_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_24" value="1" />
  <Int32 key="episode_6_level_24_contraption" value="1" />
  <Int32 key="episode_6_level_24_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_24" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_24" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_24" value="1" />
  <Int32 key="episode_6_level_24_stars" value="3" />
  <String key="episode_6_level_25_dessert_placement" value="" />
  <Boolean key="episode_6_level_25_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_25" value="1" />
  <Int32 key="episode_6_level_25_contraption" value="1" />
  <Int32 key="episode_6_level_25_challenge_0" value="2" />
  <Int32 key="episode_6_level_25_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_25" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_25" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_25" value="1" />
  <Int32 key="episode_6_level_25_stars" value="3" />
  <String key="episode_6_level_26_dessert_placement" value="DessertPlace06:StrawberryCake;DessertPlace15:VanillaCakeSlice" />
  <Boolean key="episode_6_level_26_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_26" value="1" />
  <Int32 key="episode_6_level_26_contraption" value="1" />
  <Int32 key="episode_6_level_26_challenge_0" value="2" />
  <Int32 key="episode_6_level_26_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_26" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_26" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_26" value="1" />
  <Int32 key="episode_6_level_26_stars" value="3" />
  <String key="episode_6_level_27_dessert_placement" value="DessertPlace03:IcecreamBalls;DessertPlace18:CreamyBun" />
  <Boolean key="episode_6_level_27_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_27" value="1" />
  <Int32 key="episode_6_level_27_contraption" value="1" />
  <Int32 key="episode_6_level_27_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_27" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_27" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_27" value="1" />
  <Int32 key="episode_6_level_27_stars" value="3" />
  <String key="episode_6_level_28_dessert_placement" value="DessertPlace05:VanillaCakeSlice;DessertPlace08:IcecreamBalls" />
  <Boolean key="episode_6_level_28_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_28" value="1" />
  <Int32 key="episode_6_level_28_contraption" value="1" />
  <Int32 key="episode_6_level_28_challenge_0" value="2" />
  <Int32 key="episode_6_level_28_challenge_1" value="2" />
  <Int32 key="episode_6_level_28_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_28" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_28" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_28" value="1" />
  <Int32 key="episode_6_level_28_stars" value="3" />
  <String key="episode_6_level_29_dessert_placement" value="" />
  <Boolean key="episode_6_level_29_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_29" value="1" />
  <Int32 key="episode_6_level_29_contraption" value="1" />
  <Int32 key="episode_6_level_29_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_29" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_29" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_29" value="1" />
  <Int32 key="episode_6_level_29_stars" value="3" />
  <String key="episode_6_level_30_dessert_placement" value="" />
  <Boolean key="episode_6_level_30_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_30" value="1" />
  <Int32 key="episode_6_level_30_contraption" value="1" />
  <Int32 key="episode_6_level_30_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_30" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_30" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_30" value="1" />
  <Int32 key="episode_6_level_30_stars" value="3" />
  <String key="episode_6_level_31_dessert_placement" value="" />
  <Boolean key="episode_6_level_31_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_31" value="1" />
  <Int32 key="episode_6_level_31_contraption" value="1" />
  <Int32 key="episode_6_level_31_challenge_0" value="2" />
  <Int32 key="episode_6_level_31_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_31" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_31" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_31" value="1" />
  <Int32 key="episode_6_level_31_stars" value="3" />
  <String key="episode_6_level_32_dessert_placement" value="" />
  <Int32 key="StartedLevel episode_6_level_32" value="1" />
  <Int32 key="episode_6_level_32_contraption" value="1" />
  <Int32 key="episode_6_level_32_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_32" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_32" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_32" value="1" />
  <Int32 key="episode_6_level_32_stars" value="3" />
  <Int32 key="episode_6_level_32_challenge_1" value="2" />
  <String key="episode_6_level_33_dessert_placement" value="DessertPlace13:CreamyBun;DessertPlace07:Cupcake" />
  <Boolean key="episode_6_level_33_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_33" value="1" />
  <Int32 key="episode_6_level_33_contraption" value="1" />
  <Int32 key="episode_6_level_33_challenge_0" value="2" />
  <Int32 key="episode_6_level_33_challenge_2" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_33" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_33" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_33" value="1" />
  <Int32 key="episode_6_level_33_stars" value="3" />
  <String key="episode_6_level_34_dessert_placement" value="DessertPlace08:CreamyBun;DessertPlace12:VanillaCakeSlice;DessertPlace04:VanillaCakeSlice" />
  <Boolean key="episode_6_level_34_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_34" value="1" />
  <Int32 key="episode_6_level_34_contraption" value="1" />
  <Int32 key="episode_6_level_34_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_34" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_34" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_34" value="1" />
  <Int32 key="episode_6_level_34_stars" value="3" />
  <String key="episode_6_level_35_dessert_placement" value="DessertPlace06:IcecreamBalls;DessertPlace04:CreamyBun;DessertPlace08:StrawberryCake" />
  <Boolean key="episode_6_level_35_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_35" value="1" />
  <Int32 key="episode_6_level_35_contraption" value="1" />
  <Int32 key="episode_6_level_35_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_35" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_35" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_35" value="1" />
  <Int32 key="episode_6_level_35_stars" value="3" />
  <String key="episode_6_level_36_dessert_placement" value="DessertPlace14:Cupcake" />
  <Boolean key="episode_6_level_36_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_36" value="1" />
  <Int32 key="episode_6_level_36_contraption" value="1" />
  <Int32 key="episode_6_level_36_challenge_0" value="2" />
  <Int32 key="exp_LevelComplete1Starepisode_6_level_36" value="1" />
  <Int32 key="exp_LevelComplete2Starepisode_6_level_36" value="1" />
  <Int32 key="exp_LevelComplete3Starepisode_6_level_36" value="1" />
  <Int32 key="episode_6_level_36_stars" value="3" />
  <Int32 key="Episode6_End_played" value="1" />
  <Int32 key="cr_Level_Race_01_contraption_2" value="1" />
  <Int32 key="episode_6_level_IV_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_IV" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_IV" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_IV" value="1" />
  <Int32 key="episode_6_level_IV_stars" value="3" />
  <Boolean key="episode_6_level_V_autobuild_available" value="True" />
  <String key="test51_dessert_placement" value="DessertPlace16:Cupcake" />
  <Boolean key="SECRET_DISCOVERED_test51" value="True" />
  <String key="test35_dessert_placement" value="DessertPlace16:IcecreamBalls" />
  <Boolean key="SECRET_DISCOVERED_test35" value="True" />
  <String key="test40_dessert_placement" value="DessertPlace20:VanillaCakeSlice;DessertPlace25:IcecreamBalls" />
  <Boolean key="SECRET_DISCOVERED_test40" value="True" />
  <Boolean key="SECRET_DISCOVERED_test22" value="True" />
  <Boolean key="SECRET_DISCOVERED_test26" value="True" />
  <Boolean key="SECRET_DISCOVERED_test29" value="True" />
  <Boolean key="SECRET_DISCOVERED_test33" value="True" />
  <Boolean key="SECRET_DISCOVERED_Level_27" value="True" />
  <Boolean key="SECRET_DISCOVERED_Level_29" value="True" />
  <Boolean key="Part_Pumpkin_01_SET_isUsed" value="True" />
  <Int32 key="Level_Sandbox_04_star_StarBox15" value="2" />
  <String key="Level_Sandbox_02_dessert_placement" value="DessertPlace27:Cupcake;DessertPlace33:StrawberryCake;DessertPlace69:VanillaCakeSlice;DessertPlace67:Cupcake;DessertPlace86:Cupcake;DessertPlace44:Cupcake;DessertPlace11:VanillaCakeSlice;DessertPlace12:StrawberryCake;DessertPlace72:StrawberryCake;DessertPlace73:CreamyBun" />
  <String key="Level_Sandbox_06_dessert_placement" value="DessertPlace18:StrawberryCake;DessertPlace89:IcecreamBalls;DessertPlace195:StrawberryCake;DessertPlace196:StrawberryCake;DessertPlace08:Cupcake;DessertPlace181:CreamyBun;DessertPlace93:StrawberryCake;DessertPlace190:StrawberryCake;DessertPlace124:IcecreamBalls;DessertPlace25:StrawberryCake;DessertPlace38:StrawberryCake;DessertPlace37:IcecreamBalls;DessertPlace129:Cupcake;DessertPlace46:CreamyBun;DessertPlace44:Cupcake;DessertPlace158:CreamyBun;DessertPlace23:Cupcake;DessertPlace43:CreamyBun;DessertPlace173:IcecreamBalls;DessertPlace159:IcecreamBalls;DessertPlace57:VanillaCakeSlice;DessertPlace12:StrawberryCake;DessertPlace186:Cupcake;DessertPlace154:Cupcake;DessertPlace50:StrawberryCake;DessertPlace180:CreamyBun;DessertPlace145:IcecreamBalls;DessertPlace117:Cupcake;DessertPlace131:IcecreamBalls;DessertPlace134:VanillaCakeSlice;DessertPlace160:IcecreamBalls;DessertPlace51:IcecreamBalls;DessertPlace198:IcecreamBalls;DessertPlace116:StrawberryCake;DessertPlace201:IcecreamBalls;DessertPlace62:CreamyBun;DessertPlace110:CreamyBun;DessertPlace112:StrawberryCake" />
  <Int32 key="Level_Sandbox_06_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_06" value="1" />
  <Int32 key="Level_Sandbox_06_contraption" value="1" />
  <Int32 key="Level_Sandbox_06_star_StarBox37" value="2" />
  <Int32 key="Level_Sandbox_06_stars" value="40" />
  <Int32 key="Level_Sandbox_06_star_StarBox38" value="2" />
  <Int32 key="Level_Sandbox_04_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_02_contraption" value="1" />
  <Int32 key="StartedLevel episode_6_level_V" value="1" />
  <Int32 key="episode_6_level_V_contraption" value="1" />
  <Int32 key="episode_6_level_V_challenge_0" value="2" />
  <Int32 key="episode_6_level_V_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_V" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_V" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_V" value="1" />
  <Int32 key="episode_6_level_V_stars" value="3" />
  <String key="episode_6_level_VI_dessert_placement" value="" />
  <Boolean key="episode_6_level_VI_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_VI" value="1" />
  <Int32 key="episode_6_level_VI_contraption" value="1" />
  <Int32 key="episode_6_level_VI_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_VI" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_VI" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_VI" value="1" />
  <Int32 key="episode_6_level_VI_stars" value="3" />
  <String key="episode_6_level_VII_dessert_placement" value="DessertPlace07:VanillaCakeSlice" />
  <Boolean key="episode_6_level_VII_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_VII" value="1" />
  <Int32 key="episode_6_level_VII_contraption" value="1" />
  <Int32 key="episode_6_level_VII_challenge_0" value="2" />
  <Int32 key="episode_6_level_VII_challenge_1" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_VII" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_VII" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_VII" value="1" />
  <Int32 key="episode_6_level_VII_stars" value="3" />
  <String key="episode_6_level_VIII_dessert_placement" value="" />
  <Boolean key="episode_6_level_VIII_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_VIII" value="1" />
  <Int32 key="episode_6_level_VIII_contraption" value="1" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_VIII_statue" value="True" />
  <Int32 key="episode_6_level_VIII_challenge_0" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_VIII" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_VIII" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_VIII" value="1" />
  <Int32 key="episode_6_level_VIII_stars" value="3" />
  <String key="episode_6_level_IX_dessert_placement" value="DessertPlace14:StrawberryCake;DessertPlace09:CreamyBun" />
  <Boolean key="episode_6_level_IX_autobuild_available" value="True" />
  <Int32 key="StartedLevel episode_6_level_IX" value="1" />
  <Int32 key="episode_6_level_IX_contraption" value="1" />
  <Int32 key="episode_6_level_IX_challenge_0" value="2" />
  <Int32 key="episode_6_level_IX_challenge_1" value="2" />
  <Int32 key="episode_6_level_IX_challenge_2" value="2" />
  <Int32 key="exp_JokerLevelComplete1Starepisode_6_level_IX" value="1" />
  <Int32 key="exp_JokerLevelComplete2Starepisode_6_level_IX" value="1" />
  <Int32 key="exp_JokerLevelComplete3Starepisode_6_level_IX" value="1" />
  <Int32 key="episode_6_level_IX_stars" value="3" />
  <Int32 key="Level_Sandbox_02_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_02_stars" value="20" />
  <Int32 key="Level_Sandbox_02_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_02_star_StarBox15" value="2" />
  <String key="Level_Sandbox_09_dessert_placement" value="DessertPlace21:StrawberryCake;DessertPlace115:CreamyBun;DessertPlace97:VanillaCakeSlice;DessertPlace06:Cupcake;DessertPlace69:IcecreamBalls;DessertPlace65:VanillaCakeSlice;DessertPlace42:CreamyBun;DessertPlace68:CreamyBun;DessertPlace49:CreamyBun;DessertPlace57:IcecreamBalls;DessertPlace13:Cupcake;DessertPlace33:Cupcake;DessertPlace44:IcecreamBalls;DessertPlace77:CreamyBun;DessertPlace25:VanillaCakeSlice;DessertPlace22:CreamyBun;DessertPlace75:IcecreamBalls;DessertPlace41:CreamyBun;DessertPlace76:StrawberryCake;DessertPlace62:StrawberryCake" />
  <Int32 key="Level_Sandbox_09_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_09" value="1" />
  <Int32 key="Level_Sandbox_09_contraption" value="1" />
  <Int32 key="Level_Sandbox_09_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_09_stars" value="20" />
  <Int32 key="Level_Sandbox_09_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_09_star_StarBox17" value="2" />
  <String key="Level_Sandbox_10_dessert_placement" value="DessertPlace14:StrawberryCake;DessertPlace51:Cupcake;DessertPlace63:IcecreamBalls;DessertPlace55:Cupcake;DessertPlace80:IcecreamBalls;DessertPlace17:CreamyBun;DessertPlace15:Cupcake;DessertPlace61:CreamyBun;DessertPlace34:VanillaCakeSlice;DessertPlace73:IcecreamBalls" />
  <Int32 key="Level_Sandbox_10_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_10" value="1" />
  <Int32 key="Level_Sandbox_10_contraption" value="1" />
  <Int32 key="Level_Sandbox_10_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_10_stars" value="20" />
  <Int32 key="Level_Sandbox_10_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_10_star_StarBox12" value="2" />
  <String key="Level_Sandbox_03_dessert_placement" value="DessertPlace40:Cupcake;DessertPlace49:StrawberryCake;DessertPlace61:CreamyBun;DessertPlace68:IcecreamBalls;DessertPlace62:Cupcake;DessertPlace27:VanillaCakeSlice;DessertPlace80:VanillaCakeSlice;DessertPlace82:Cupcake;DessertPlace29:Cupcake;DessertPlace26:StrawberryCake" />
  <Int32 key="Level_Sandbox_03_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_03" value="1" />
  <Int32 key="Level_Sandbox_03_contraption" value="1" />
  <Int32 key="Level_Sandbox_03_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_03_stars" value="20" />
  <Int32 key="Level_Sandbox_03_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_03_star_StarBox01" value="2" />
  <String key="Level_Sandbox_05_dessert_placement" value="DessertPlace75:VanillaCakeSlice;DessertPlace17:VanillaCakeSlice;DessertPlace80:Cupcake;DessertPlace16:IcecreamBalls;DessertPlace70:StrawberryCake;DessertPlace26:VanillaCakeSlice;DessertPlace15:Cupcake;DessertPlace31:VanillaCakeSlice;DessertPlace62:Cupcake;DessertPlace84:IcecreamBalls" />
  <Int32 key="Level_Sandbox_05_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_05" value="1" />
  <Int32 key="Level_Sandbox_05_contraption" value="1" />
  <Int32 key="Level_Sandbox_05_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_05_stars" value="20" />
  <Int32 key="Level_Sandbox_05_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_05_star_StarBox20" value="2" />
  <String key="Level_Sandbox_07_dessert_placement" value="DessertPlace01:CreamyBun;DessertPlace03:IcecreamBalls;DessertPlace38:StrawberryCake;DessertPlace81:CreamyBun;DessertPlace37:VanillaCakeSlice;DessertPlace23:StrawberryCake;DessertPlace58:CreamyBun;DessertPlace21:VanillaCakeSlice;DessertPlace44:Cupcake;DessertPlace34:VanillaCakeSlice" />
  <Int32 key="Level_Sandbox_07_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_07" value="1" />
  <Int32 key="Level_Sandbox_07_contraption" value="1" />
  <Int32 key="Level_Sandbox_07_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_07_stars" value="20" />
  <Int32 key="Level_Sandbox_07_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_07_star_StarBox02" value="2" />
  <String key="Level_Sandbox_08_dessert_placement" value="DessertPlace53:VanillaCakeSlice;DessertPlace79:CreamyBun;DessertPlace186:Cupcake;DessertPlace30:VanillaCakeSlice;DessertPlace62:IcecreamBalls;DessertPlace173:CreamyBun;DessertPlace125:StrawberryCake;DessertPlace193:StrawberryCake;DessertPlace172:StrawberryCake;DessertPlace31:VanillaCakeSlice;DessertPlace203:IcecreamBalls;DessertPlace74:StrawberryCake;DessertPlace148:VanillaCakeSlice;DessertPlace179:CreamyBun;DessertPlace157:StrawberryCake;DessertPlace123:StrawberryCake;DessertPlace201:StrawberryCake;DessertPlace73:StrawberryCake;DessertPlace43:StrawberryCake;DessertPlace12:Cupcake" />
  <Int32 key="Level_Sandbox_08_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_08" value="1" />
  <Int32 key="Level_Sandbox_08_contraption" value="1" />
  <Int32 key="Level_Sandbox_08_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_08_stars" value="20" />
  <Int32 key="Level_Sandbox_08_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_08_star_StarBox19" value="2" />
  <String key="Level_Sandbox_01_dessert_placement" value="DessertPlace63:StrawberryCake;DessertPlace64:CreamyBun;DessertPlace68:CreamyBun;DessertPlace56:CreamyBun;DessertPlace06:IcecreamBalls;DessertPlace89:IcecreamBalls;DessertPlace34:VanillaCakeSlice;DessertPlace82:VanillaCakeSlice;DessertPlace55:StrawberryCake;DessertPlace54:StrawberryCake" />
  <Int32 key="Level_Sandbox_01_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Level_Sandbox_01" value="1" />
  <Int32 key="Level_Sandbox_01_contraption" value="1" />
  <Int32 key="Level_Sandbox_01_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_01_stars" value="20" />
  <Int32 key="Level_Sandbox_01_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox07" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_01_star_StarBox10" value="2" />
  <String key="Episode_6_Tower Sandbox_dessert_placement" value="DessertPlace06:StrawberryCake;DessertPlace26:CreamyBun;DessertPlace23:StrawberryCake;DessertPlace08:CreamyBun;DessertPlace16:StrawberryCake;DessertPlace29:Cupcake;DessertPlace30:CreamyBun;DessertPlace12:IcecreamBalls;DessertPlace24:CreamyBun;DessertPlace04:StrawberryCake;DessertPlace21:VanillaCakeSlice;DessertPlace18:Cupcake;DessertPlace20:StrawberryCake;DessertPlace05:VanillaCakeSlice;DessertPlace19:VanillaCakeSlice" />
  <Int32 key="Episode_6_Tower Sandbox_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="Episode_6_Tower Sandbox_contraption" value="1" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox04" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_stars" value="20" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox03" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox08" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_DynamicStarBox" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox10" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox01" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox09" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox07" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox02" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox08" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox03" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox05" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox11" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox06" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox04" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox05" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox02" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox06" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_StarBox07" value="2" />
  <Int32 key="Episode_6_Tower Sandbox_star_FloatingStarBox01" value="2" />
  <String key="Episode_6_Ice Sandbox_dessert_placement" value="DessertPlace06:CreamyBun;DessertPlace28:CreamyBun;DessertPlace20:IcecreamBalls" />
  <Int32 key="Episode_6_Ice Sandbox_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Episode_6_Ice Sandbox" value="1" />
  <Int32 key="Episode_6_Ice Sandbox_contraption" value="1" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox13" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_stars" value="20" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox01" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox10" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox06" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox08" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox07" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox02" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox09" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox03" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox11" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox01" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox04" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox06" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox03" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox12" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox02" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox07" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_FloatingStarBox05" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox05" value="2" />
  <Int32 key="Episode_6_Ice Sandbox_star_StarBox04" value="2" />
  <String key="Episode_6_Dark Sandbox_dessert_placement" value="DessertPlace24:StrawberryCake;DessertPlace22:VanillaCakeSlice;DessertPlace23:CreamyBun;DessertPlace16:StrawberryCake;DessertPlace03:StrawberryCake;DessertPlace02:Cupcake;DessertPlace04:CreamyBun;DessertPlace05:StrawberryCake;DessertPlace21:IcecreamBalls;DessertPlace18:VanillaCakeSlice;DessertPlace26:VanillaCakeSlice;DessertPlace15:StrawberryCake" />
  <Int32 key="Episode_6_Dark Sandbox_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel Episode_6_Dark Sandbox" value="1" />
  <Int32 key="Episode_6_Dark Sandbox_contraption" value="1" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox14" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_stars" value="20" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox19" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox18" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox16" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox09" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox04" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_FloatingStarBox01" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox01" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox17" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox15" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox20" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox12" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_FloatingStarBox02" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox07" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox11" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox10" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox05" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox03" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox13" value="2" />
  <Int32 key="Episode_6_Dark Sandbox_star_StarBox02" value="2" />
  <String key="MMSandbox_dessert_placement" value="DessertPlace02:VanillaCakeSlice;DessertPlace36:CreamyBun;DessertPlace117:VanillaCakeSlice;DessertPlace16:StrawberryCake;DessertPlace69:StrawberryCake;DessertPlace22:IcecreamBalls;DessertPlace47:IcecreamBalls;DessertPlace78:IcecreamBalls;DessertPlace114:Cupcake;DessertPlace48:IcecreamBalls;DessertPlace81:CreamyBun;DessertPlace115:Cupcake;DessertPlace103:Cupcake;DessertPlace15:CreamyBun;DessertPlace25:IcecreamBalls;DessertPlace04:VanillaCakeSlice;DessertPlace92:Cupcake;DessertPlace59:StrawberryCake;DessertPlace61:IcecreamBalls;DessertPlace09:VanillaCakeSlice" />
  <Int32 key="MMSandbox_LastLoadedContraptionSlotIndex" value="0" />
  <Int32 key="StartedLevel MMSandbox" value="1" />
  <Int32 key="MMSandbox_contraption" value="1" />
  <Int32 key="MMSandbox_star_PartBox_002" value="2" />
  <Int32 key="MMSandbox_stars" value="40" />
  <Int32 key="MMSandbox_part_PartBox_002" value="1" />
  <Int32 key="MMSandbox_parts" value="40" />
  <Int32 key="MMSandbox_part_unlocked_SpringBoxingGlove" value="4" />
  <Int32 key="MMSandbox_part_SpringBoxingGlove" value="4" />
  <Int32 key="MMSandbox_star_FloatingPartBox_003" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_003" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Rocket" value="6" />
  <Int32 key="MMSandbox_part_Rocket" value="6" />
  <Int32 key="MMSandbox_star_FloatingPartBox_002" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_002" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Rotor" value="4" />
  <Int32 key="MMSandbox_part_Rotor" value="4" />
  <Int32 key="MMSandbox_star_PartBox_018" value="2" />
  <Int32 key="MMSandbox_part_PartBox_018" value="1" />
  <Int32 key="MMSandbox_part_unlocked_GrapplingHook" value="4" />
  <Int32 key="MMSandbox_part_GrapplingHook" value="4" />
  <Int32 key="MMSandbox_star_PartBox_006" value="2" />
  <Int32 key="MMSandbox_part_PartBox_006" value="1" />
  <Int32 key="MMSandbox_part_unlocked_NormalWheel" value="4" />
  <Int32 key="MMSandbox_part_NormalWheel" value="4" />
  <Int32 key="MMSandbox_star_PartBox_003" value="2" />
  <Int32 key="MMSandbox_part_PartBox_003" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Gearbox" value="1" />
  <Int32 key="MMSandbox_part_Gearbox" value="1" />
  <Int32 key="MMSandbox_star_PartBox_020" value="2" />
  <Int32 key="MMSandbox_part_PartBox_020" value="1" />
  <Int32 key="MMSandbox_part_unlocked_MotorWheel" value="6" />
  <Int32 key="MMSandbox_part_MotorWheel" value="6" />
  <Int32 key="MMSandbox_star_DynamicPartBox_002" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_002" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Propeller" value="5" />
  <Int32 key="MMSandbox_part_Propeller" value="5" />
  <Int32 key="MMSandbox_star_DynamicPartBox_004" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_004" value="1" />
  <Int32 key="MMSandbox_part_unlocked_SmallWheel" value="6" />
  <Int32 key="MMSandbox_part_SmallWheel" value="6" />
  <Int32 key="MMSandbox_star_FloatingPartBox_008" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_008" value="1" />
  <Int32 key="MMSandbox_part_unlocked_StickyWheel" value="4" />
  <Int32 key="MMSandbox_part_StickyWheel" value="4" />
  <Int32 key="MMSandbox_star_PartBox_005" value="2" />
  <Int32 key="MMSandbox_part_PartBox_005" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Spring" value="4" />
  <Int32 key="MMSandbox_part_Spring" value="4" />
  <Int32 key="MMSandbox_star_FloatingPartBox_004" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_004" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Balloons3" value="4" />
  <Int32 key="MMSandbox_part_Balloons3" value="4" />
  <Int32 key="MMSandbox_star_PartBox_008" value="2" />
  <Int32 key="MMSandbox_part_PartBox_008" value="1" />
  <Int32 key="MMSandbox_part_unlocked_TNT" value="10" />
  <Int32 key="MMSandbox_part_TNT" value="10" />
  <Int32 key="MMSandbox_star_FloatingPartBox_007" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_007" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Kicker" value="6" />
  <Int32 key="MMSandbox_part_Kicker" value="6" />
  <Int32 key="MMSandbox_star_FloatingPartBox_001" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_001" value="1" />
  <Int32 key="MMSandbox_part_unlocked_PoweredUmbrella" value="4" />
  <Int32 key="MMSandbox_part_PoweredUmbrella" value="4" />
  <Int32 key="MMSandbox_star_PartBox_001" value="2" />
  <Int32 key="MMSandbox_part_PartBox_001" value="1" />
  <Int32 key="MMSandbox_star_PartBox_016" value="2" />
  <Int32 key="MMSandbox_part_PartBox_016" value="1" />
  <Int32 key="MMSandbox_part_unlocked_EngineBig" value="6" />
  <Int32 key="MMSandbox_part_EngineBig" value="6" />
  <Int32 key="MMSandbox_star_PartBox_017" value="2" />
  <Int32 key="MMSandbox_part_PartBox_017" value="1" />
  <Int32 key="MMSandbox_star_PartBox_019" value="2" />
  <Int32 key="MMSandbox_part_PartBox_019" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Engine" value="3" />
  <Int32 key="MMSandbox_part_Engine" value="3" />
  <Int32 key="MMSandbox_star_PartBox_022" value="2" />
  <Int32 key="MMSandbox_part_PartBox_022" value="1" />
  <Int32 key="MMSandbox_star_PartBox_004" value="2" />
  <Int32 key="MMSandbox_part_PartBox_004" value="1" />
  <Int32 key="MMSandbox_part_unlocked_MetalFrame" value="17" />
  <Int32 key="MMSandbox_part_MetalFrame" value="17" />
  <Int32 key="MMSandbox_star_PartBox_013" value="2" />
  <Int32 key="MMSandbox_part_PartBox_013" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Egg" value="1" />
  <Int32 key="MMSandbox_part_Egg" value="1" />
  <Int32 key="MMSandbox_star_PartBox_021" value="2" />
  <Int32 key="MMSandbox_part_PartBox_021" value="1" />
  <Int32 key="MMSandbox_star_FloatingPartBox_005" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_005" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Sandbag2" value="4" />
  <Int32 key="MMSandbox_part_Sandbag2" value="4" />
  <Int32 key="MMSandbox_star_PartBox_007" value="2" />
  <Int32 key="MMSandbox_part_PartBox_007" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Umbrella" value="6" />
  <Int32 key="MMSandbox_part_Umbrella" value="6" />
  <Int32 key="MMSandbox_star_DynamicPartBox_001" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_001" value="1" />
  <Int32 key="MMSandbox_star_PartBox_010" value="2" />
  <Int32 key="MMSandbox_part_PartBox_010" value="1" />
  <Int32 key="MMSandbox_part_unlocked_WoodenFrame" value="10" />
  <Int32 key="MMSandbox_part_WoodenFrame" value="10" />
  <Int32 key="MMSandbox_star_FloatingPartBox_009" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_009" value="1" />
  <Int32 key="MMSandbox_star_PartBox_011" value="2" />
  <Int32 key="MMSandbox_part_PartBox_011" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Pumpkin" value="6" />
  <Int32 key="MMSandbox_part_Pumpkin" value="6" />
  <Int32 key="MMSandbox_star_PartBox_014" value="2" />
  <Int32 key="MMSandbox_part_PartBox_014" value="1" />
  <Int32 key="MMSandbox_star_PartBox_015" value="2" />
  <Int32 key="MMSandbox_part_PartBox_015" value="1" />
  <Int32 key="MMSandbox_star_FloatingPartBox_006" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_006" value="1" />
  <Int32 key="MMSandbox_star_PartBox_012" value="2" />
  <Int32 key="MMSandbox_part_PartBox_012" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Rope" value="6" />
  <Int32 key="MMSandbox_part_Rope" value="6" />
  <Int32 key="MMSandbox_star_PartBox_009" value="2" />
  <Int32 key="MMSandbox_part_PartBox_009" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Sandbag3" value="4" />
  <Int32 key="MMSandbox_part_Sandbag3" value="4" />
  <Int32 key="MMSandbox_star_DynamicPartBox_003" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_003" value="1" />
  <Int32 key="MMSandbox_part_unlocked_MetalTail" value="4" />
  <Int32 key="MMSandbox_part_MetalTail" value="4" />
  <Int32 key="MMSandbox_star_DynamicPartBox_007" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_007" value="1" />
  <Int32 key="MMSandbox_part_unlocked_MetalWing" value="4" />
  <Int32 key="MMSandbox_part_MetalWing" value="4" />
  <Int32 key="MMSandbox_star_DynamicPartBox_005" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_005" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Tailplane" value="4" />
  <Int32 key="MMSandbox_part_Tailplane" value="4" />
  <Int32 key="MMSandbox_star_DynamicPartBox_008" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_008" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Sandbag" value="4" />
  <Int32 key="MMSandbox_part_Sandbag" value="4" />
  <Int32 key="MMSandbox_star_DynamicPartBox_006" value="2" />
  <Int32 key="MMSandbox_part_DynamicPartBox_006" value="1" />
  <Int32 key="MMSandbox_part_unlocked_Wings" value="4" />
  <Int32 key="MMSandbox_part_Wings" value="4" />
  <Boolean key="FlurryEventSent_All non-IAP Content Played" value="True" />
  <Boolean key="FlurryEventSent_All Content Played" value="True" />
  <Int32 key="MMSandbox_star_FloatingPartBox_010" value="2" />
  <Int32 key="MMSandbox_part_FloatingPartBox_010" value="1" />
  <Int32 key="MMSandbox_part_unlocked_RedRocket" value="6" />
  <Int32 key="MMSandbox_part_RedRocket" value="6" />
  <Int32 key="Level_Sandbox_06_star_StarBox18" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox19" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox17" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox09" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox20" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox08" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox05" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox02" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox16" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox35" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox40" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox21" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox22" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox23" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox03" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox26" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox34" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox28" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox29" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox33" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox12" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox27" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox25" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox24" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox32" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox39" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox31" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox14" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox36" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox30" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox15" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox13" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox04" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox01" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox10" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox11" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox06" value="2" />
  <Int32 key="Level_Sandbox_06_star_StarBox07" value="2" />
  <Int32 key="part_Balloons2" value="99" />
  <Int32 key="part_Balloon" value="99" />
  <String key="LootCrateSlot_1" value="Inactive,Glass" />
  <String key="LootCrateSlot_3" value="Locked,Glass" />
  <Int32 key="part_Balloons3" value="99" />
  <Int32 key="part_Fan" value="99" />
  <Int32 key="part_WoodenFrame" value="99" />
  <Int32 key="part_Bellows" value="99" />
  <Int32 key="part_CartWheel" value="99" />
  <Int32 key="part_Basket" value="99" />
  <Int32 key="part_Sandbag" value="99" />
  <Int32 key="part_Pig" value="99" />
  <Int32 key="part_Sandbag2" value="99" />
  <Int32 key="part_Sandbag3" value="99" />
  <Int32 key="part_Propeller" value="99" />
  <Int32 key="part_Wings" value="99" />
  <Int32 key="part_Tailplane" value="99" />
  <Int32 key="part_Engine" value="99" />
  <Int32 key="part_Rocket" value="99" />
  <Int32 key="part_MetalFrame" value="99" />
  <Int32 key="part_SmallWheel" value="99" />
  <Int32 key="part_MetalWing" value="99" />
  <Int32 key="part_MetalTail" value="99" />
  <Int32 key="part_Rotor" value="99" />
  <Int32 key="part_MotorWheel" value="99" />
  <Int32 key="part_TNT" value="99" />
  <Int32 key="part_EngineSmall" value="99" />
  <Int32 key="part_EngineBig" value="99" />
  <Int32 key="part_NormalWheel" value="99" />
  <Int32 key="part_Spring" value="99" />
  <Int32 key="part_Umbrella" value="99" />
  <Int32 key="part_Rope" value="99" />
  <Int32 key="part_CokeBottle" value="99" />
  <Int32 key="part_KingPig" value="99" />
  <Int32 key="part_RedRocket" value="99" />
  <Int32 key="part_SodaBottle" value="99" />
  <Int32 key="part_PoweredUmbrella" value="99" />
  <Int32 key="part_Egg" value="99" />
  <Int32 key="part_SpringBoxingGlove" value="99" />
  <Int32 key="part_StickyWheel" value="99" />
  <Int32 key="part_GrapplingHook" value="99" />
  <Int32 key="part_Pumpkin" value="99" />
  <Int32 key="part_Kicker" value="99" />
  <Int32 key="part_Gearbox" value="99" />
  <Int32 key="part_GoldenPig" value="99" />
  <Int32 key="part_PointLight" value="99" />
  <Int32 key="part_SpotLight" value="99" />
  <Int32 key="part_TimeBomb" value="99" />
  <Int32 key="part_MAX" value="99" />
  <Int32 key="episode_6_level_4_challenge_2" value="2" />
  <Int32 key="episode_6_level_13_challenge_2" value="2" />
  <String key="Level_24_dessert_placement" value="DessertPlace03:CreamyBun;DessertPlace10:VanillaCakeSlice" />
  <Int32 key="scenario_27_challenge_2" value="2" />
  <String key="LootCrateSlot_2" value="Inactive,Cardboard" />
  <Boolean key="SECRET_DISCOVERED_scenario_72" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_75" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_87" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_92" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_90" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_58" value="True" />
  <Boolean key="SECRET_DISCOVERED_track_29" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_80" value="True" />
  <Boolean key="SECRET_DISCOVERED_track_12" value="True" />
  <Boolean key="SECRET_DISCOVERED_Level_03" value="True" />
  <Boolean key="SECRET_DISCOVERED_Level_07" value="True" />
  <Boolean key="SECRET_DISCOVERED_test01" value="True" />
  <Boolean key="SECRET_DISCOVERED_test06" value="True" />
  <Boolean key="SECRET_DISCOVERED_Level_38" value="True" />
  <Int32 key="Level_38_challenge_2" value="2" />
  <Boolean key="SECRET_DISCOVERED_Level_06" value="True" />
  <Boolean key="SECRET_DISCOVERED_test08" value="True" />
  <Boolean key="SECRET_DISCOVERED_test18" value="True" />
  <Boolean key="SECRET_DISCOVERED_test12" value="True" />
  <Boolean key="SECRET_DISCOVERED_test20" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_18" value="True" />
  <Boolean key="SECRET_DISCOVERED_test59" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_39" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_56" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_25" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_38" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_30" value="True" />
  <Boolean key="SECRET_DISCOVERED_track_06" value="True" />
  <Boolean key="SECRET_DISCOVERED_test57" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_31" value="True" />
  <Boolean key="SECRET_DISCOVERED_test30" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_98" value="True" />
  <Boolean key="SECRET_DISCOVERED_scenario_06" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_5_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_6_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_7_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_8_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_II_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_17_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_19_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_V_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_29_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_30_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_31_statue" value="True" />
  <Boolean key="SECRET_DISCOVERED_episode_6_level_32_statue" value="True" />
  <Int32 key="scenario_81_challenge_2" value="2" />
</data>
