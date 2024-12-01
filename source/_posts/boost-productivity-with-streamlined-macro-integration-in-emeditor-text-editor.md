---
title: Boost Productivity with Streamlined Macro Integration in EmEditor Text Editor
date: 2024-11-29T23:08:00.394Z
updated: 2024-12-01T02:18:04.914Z
tags:
  - product
categories:
  - emeditor
thumbnail: https://thmb.techidaily.com/5a6b81e19407a604be22bf69df443b0f8b7b5bc4d3841b542775d6677ac13b8e.jpg
---

## Boost Productivity with Streamlined Macro Integration in EmEditor Text Editor

Viewing 8 posts - 1 through 8 (of 8 total)

* Author  
Posts
* April 21, 2008 at 4:16 pm [#5674](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/2e1c9efc2430993c71be903dc5b131c3?s=80&d=identicon&r=g)owilsky](https://www.emeditor.com/forums/users/owilsky/ "View owilsky's profile")  
Participant  
Hi,  
 This one is both a cry for help as well as a feature request:  
 I created some kind of IDE out of EmEditor for our company.  
 Therefor I created a lot of macros.  
 Unfortunately because of the way EmEditor stores its configuration it is very difficult to deploy and update the macros on all machines:  
 – First I install EmEditor  
 – Then I import a .reg file containing the config that everybody should use  
 – Then the problems begins: Our macros are stored in C:Documents and Settings\[username\]Application DataMy Macros.  
 So you see: Every user has another folder where the macros are saved. So I wrote a tool to change the paths in “HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3Macros”.  
 Then I saw that the keyboard shortcuts are saved in a binary field in HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3Config\[Config Name\]PIKM and that this binary field contains the absolute path in binary form —> **arghhh!!!**  
 Is there an easier way to do this? (User PCs don’t have admin rights for working, so I prefer saving macros in profile folders because they are updated quite often)  
 And please consider an easier way to store the configuration in upcoming versions.  
 Thanks for any help,  
 Oliver  
April 21, 2008 at 8:39 pm [#5677](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/a0a6377144ed3636f985d87303f65ed2?s=80&d=identicon&r=g)Yutaka Emura](https://www.emeditor.com/forums/users/yemura/ "View Yutaka Emura's profile")  
Keymaster  
> owilsky wrote:  
> Hi,  
>  
> This one is both a cry for help as well as a feature request:  
>  
> I created some kind of IDE out of EmEditor for our company.  
> Therefor I created a lot of macros.  
> Unfortunately because of the way EmEditor stores its configuration it is very difficult to deploy and update the macros on all machines:  
>  
> – First I install EmEditor  
> – Then I import a .reg file containing the config that everybody should use  
> – Then the problems begins: Our macros are stored in C:Documents and Settings\[username\]Application DataMy Macros.  
> So you see: Every user has another folder where the macros are saved. So I wrote a tool to change the paths in “HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3Macros”.  
> Then I saw that the keyboard shortcuts are saved in a binary field in HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3Config\[Config Name\]PIKM and that this binary field contains the absolute path in binary form —> **arghhh!!!**  
>  
> Is there an easier way to do this? (User PCs don’t have admin rights for working, so I prefer saving macros in profile folders because they are updated quite often)  
> And please consider an easier way to store the configuration in upcoming versions.  
>  
> Thanks for any help,  
> Oliver  
 One option is use INI file settings, which use relative path, but if My Macro folder is under user profile (sucn as UsersJohnDocuments…), you will still have to fix each relative path.  
 Another option is to use a macro, but this too can take some time. Just in case you want to try this option, I wrote the sample macro to start with:  
    
	    
	bAllConfigs = confirm("Do you want to set keyboard in ALL configurations? Click Cancel if you want to set keyboard only in the current configuration.");  
	    
	if(bAllConfigs){  
		cfgs = new Enumerator(editor.Configs);  
		for(; !cfgs.atEnd(); cfgs.moveNext()){  
		    cfg = cfgs.item();  
		    SetKeys(cfg);  

	else {  
		cfg = document.Config;  
		SetKeys(cfg);  

	alert("Keyboard set successfully!");  
	    
	function SetKeys(cfg)  

		lst = cfg.Keyboard.List;  
		// nKey is a virtual key for the shortcut.  
		// nFlags is a combination of eeVirtualKey, eeShift, eeCtrl, and eeAlt.  See the Macro Reference.  
		// nCmd is the command ID for the macro (9216 through 9216 + 1023).  You can use editor.QueryStringByID method to find the exact command ID.  
		lst.Add(nKey, nFlags, nCmd);  
		cfg.Save();  

	 For the next major version, I will try to find a way to transfer the settings, possibly by adding something like \\%MYMACRO\_PATH\\% environment, which can be included in the macro path, so the shortcut settings will be easily transferred to another PC.  
April 21, 2008 at 8:54 pm [#5679](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/2e1c9efc2430993c71be903dc5b131c3?s=80&d=identicon&r=g)owilsky](https://www.emeditor.com/forums/users/owilsky/ "View owilsky's profile")  
Participant  
> One option is use INI file settings, which use relative path, but if My Macro folder is under user profile (sucn as UsersJohnDocuments…), you will still have to fix each relative path.  
 But the ini file is saved in EmEditor’s folder in “Program Files”, right? And a normal user does not have the right to write into that folder, so he cannot save his settings into the ini file.  
 Or is the ini file located elsewhere? I though ini files are for using EmEditor on USB sticks…  
 And you cannot reimport exported ini files.  
> For the next major version, I will try to find a way to transfer the settings, possibly by adding something like \\%MYMACRO\_PATH\\% environment, which can be included in the macro path, so the shortcut settings will be easily transferred to another PC.  
 That would be fine.  
 For now I think I will go the macro way. I wrote >30 macros for our script language, so one more won’t hurt. Thanks a lot for the example.  
April 21, 2008 at 9:38 pm [#5681](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/a0a6377144ed3636f985d87303f65ed2?s=80&d=identicon&r=g)Yutaka Emura](https://www.emeditor.com/forums/users/yemura/ "View Yutaka Emura's profile")  
Keymaster  
> owilsky wrote:  
> \[But the ini file is saved in EmEditor’s folder in Program Files, right? And a normal user does not have the right to write into that folder, so he cannot save his settings into the ini file.  
 That is true. I was assuming you might want to install EmEditor to an unrestricted folder.  
April 22, 2008 at 3:52 pm [#5682](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/2e1c9efc2430993c71be903dc5b131c3?s=80&d=identicon&r=g)owilsky](https://www.emeditor.com/forums/users/owilsky/ "View owilsky's profile")  
Participant  
OK, I managed to import all keyboard shortcuts by macro. No problem, thanks for that.  
 BUT: Next problem: :-(
 In HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3CommonMainMenu my changed main menu including some macros is saved, again with macro paths hard coded. :-x  
 I guess it’s not possible to change the main menu per macro?  
 I tried to decode the main menu entry, seems to be unicode, always ansi code in hex and then “00”.  
 I tried to replace my old path with the new one in this hex field and that seemed to work great, but now I get a crash at offset 0003afb1 when I start EmEditor.  
 Guess it’s not that easy :-(
 a. Is it possible to change the main menu per macro?  
 b. If not, what’s the format of the MainMenu registry entry?  
 Thanks for any info.  
 Oliver  
April 22, 2008 at 8:52 pm [#5683](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/a0a6377144ed3636f985d87303f65ed2?s=80&d=identicon&r=g)Yutaka Emura](https://www.emeditor.com/forums/users/yemura/ "View Yutaka Emura's profile")  
Keymaster  
> owilsky wrote:  
> OK, I managed to import all keyboard shortcuts by macro. No problem, thanks for that.  
>  
> BUT: Next problem: :-(
> In HKEY\_CURRENT\_USERSoftwareEmSoftEmEditor v3CommonMainMenu my changed main menu including some macros is saved, again with macro paths hard coded. :-x  
> I guess it’s not possible to change the main menu per macro?  
>  
> I tried to decode the main menu entry, seems to be unicode, always ansi code in hex and then “00”.  
> I tried to replace my old path with the new one in this hex field and that seemed to work great, but now I get a crash at offset 0003afb1 when I start EmEditor.  
> Guess it’s not that easy :-(
>  
> a. Is it possible to change the main menu per macro?  
> b. If not, what’s the format of the MainMenu registry entry?  
>  
> Thanks for any info.  
> Oliver  
 You cannot change the macro path from the Registry. The Registry format also includes the length of each menu or command path, so it is not easy to change the Registry value. You should use the “Tools” > “Customize Menus” to change each menu item.  
April 22, 2008 at 9:12 pm [#5684](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/2e1c9efc2430993c71be903dc5b131c3?s=80&d=identicon&r=g)owilsky](https://www.emeditor.com/forums/users/owilsky/ "View owilsky's profile")  
Participant  
I cannot tell my users to install 30 macros by hand and configure 20 keyboard shortcuts for them and create their own menus.  
 If it cannot be done automatically, I will try to find out how to change the reg value. Can you tell me how the general format is? I only need the format for the macros, I do not need the “normal” menu commands.  
 I guess there must be 3 parts per macro:  
 – path and filename of macro  
 – keyboard shortcut  
 – as you said the length of the entry.  
 – plus maybe a separator between different entries?  
 It may be difficult but I know I can do it!  
 Oliver  
April 23, 2008 at 4:38 am [#5685](https://tools.techidaily.com/emeditor/products/)  
[![](https://secure.gravatar.com/avatar/a0a6377144ed3636f985d87303f65ed2?s=80&d=identicon&r=g)Yutaka Emura](https://www.emeditor.com/forums/users/yemura/ "View Yutaka Emura's profile")  
Keymaster  
> owilsky wrote:  
> I cannot tell my users to install 30 macros by hand and configure 20 keyboard shortcuts for them and create their own menus.  
> If it cannot be done automatically, I will try to find out how to change the reg value. Can you tell me how the general format is? I only need the format for the macros, I do not need the “normal” menu commands.  
> I guess there must be 3 parts per macro:  
> – path and filename of macro  
> – keyboard shortcut  
> – as you said the length of the entry.  
> – plus maybe a separator between different entries?  
>  
> It may be difficult but I know I can do it!  
>  
> Oliver  
 Here is the source code for writing a menu to the registry. I know you will have a lot of questions, but I hope you can figure them out. Ignore T2E and CV\_ACP.  
    
	BOOL SaveMenuItem(CMenuArray& MenuArray, int nMenuKind, bool bDelete)  

		HKEY hKey = GetCommonRootKey();  
		if(hKey == NULL)  return FALSE;  
		BOOL bSuccess = FALSE;  
		if(bDelete){  
			MyRegDeleteValue(hKey, aszMenu[nMenuKind]);  
			bSuccess = TRUE;  

		else {  
			int nLen;  
			DWORD dwCount = sizeof(int);  
			dwCount += sizeof(DWORD);  
			CMenuArray::iterator it = MenuArray.begin();  
			int nMax = 0;  
			while(it != MenuArray.end()){  
				CV_ACP;  
				dwCount += (DWORD)wcslen(T2E(it->m_szName)) * sizeof(WCHAR);  
				dwCount += (DWORD)wcslen(T2E(it->m_szFile)) * sizeof(WCHAR);  
				dwCount += sizeof(int) + sizeof(UINT) + sizeof(int) + sizeof(int);  
				nMax++;  
				it++;  

			char* pBuf = new char[dwCount];  
			if(pBuf != NULL){  
				char* p = pBuf;  
				*((DWORD*)p) = SIGNATURE_MENU_LIST_2;  
				p += sizeof(DWORD);  
				*((int*)p) = nMax;  
				p += sizeof(int);  
				it = MenuArray.begin();  
				while(it != MenuArray.end()){  
					*((UINT*)p) = it->m_nID;  
					p += sizeof(UINT);  
					*p = (char)it->m_nDepth;  
					p += sizeof(UINT);  
					CV_ACP;  
					LPWSTR szE = T2E(it->m_szName);  
					nLen = (int)wcslen(szE);  
					*((int*)p) = nLen;  
					p += sizeof(int);  
					memcpy(p, szE, nLen * sizeof(WCHAR));  
					p += nLen * sizeof(WCHAR);  
	    
					szE = T2E(it->m_szFile);  
					nLen = (int)wcslen(szE);  
					*((int*)p) = nLen;  
					p += sizeof(int);  
					memcpy(p, szE, nLen * sizeof(WCHAR));  
					p += nLen * sizeof(WCHAR);  
	    
					it++;  

				ASSERT(p == pBuf + dwCount);  
				bSuccess = (p == pBuf + dwCount);  
				WriteProfileBinaryReg(hKey, aszMenu[nMenuKind], (LPBYTE)pBuf, dwCount);  
				delete [] pBuf;  

		MyRegCloseKey(hKey);  
		return bSuccess;  

	 P.S. How about creating a popup menu using PopupMenu object in the macro?  
[http://www.emeditor.com/help/macro/popupmenu/index.htm](https://tools.techidaily.com/emeditor/products/)
* Author  
Posts

Viewing 8 posts - 1 through 8 (of 8 total)

* You must be logged in to reply to this topic.

<ins class="adsbygoogle"
     style="display:block"
     data-ad-format="autorelaxed"
     data-ad-client="ca-pub-7571918770474297"
     data-ad-slot="1223367746"></ins>

<ins class="adsbygoogle"
     style="display:block"
     data-ad-client="ca-pub-7571918770474297"
     data-ad-slot="8358498916"
     data-ad-format="auto"
     data-full-width-responsive="true"></ins>

<span class="atpl-alsoreadstyle">Also read:</span>
<div><ul>
<li><a href="https://facebook-record-videos.techidaily.com/new-2024-approved-elevate-youtube-presence-ideal-release-windows/"><u>[New] 2024 Approved Elevate Youtube Presence Ideal Release Windows</u></a></li>
<li><a href="https://eaxpv-info.techidaily.com/new-2024-approved-fast-track-video-scaling-for-perfect-mac-display/"><u>[New] 2024 Approved Fast-Track Video Scaling for Perfect Mac Display</u></a></li>
<li><a href="https://screen-capture.techidaily.com/new-in-2024-the-path-to-flawless-film-recording-device-agnostic-guide/"><u>[New] In 2024, The Path to Flawless Film Recording Device Agnostic Guide</u></a></li>
<li><a href="https://win-best.techidaily.com/effortless-installation-of-windows-10-onto-a-new-ssd-via-usb-two-simple-methods/"><u>Effortless Installation of Windows 10 Onto a New SSD via USB: Two Simple Methods</u></a></li>
<li><a href="https://win-best.techidaily.com/exploring-the-efficacy-of-remo-recover-a-comprehensive-review/"><u>Exploring the Efficacy of Remo Recover: A Comprehensive Review</u></a></li>
<li><a href="https://blog-min.techidaily.com/how-to-migrate-android-data-from-vivo-y100a-to-new-android-phone-drfone-by-drfone-transfer-from-android-transfer-from-android/"><u>How to Migrate Android Data From Vivo Y100A to New Android Phone? | Dr.fone</u></a></li>
<li><a href="https://iphone-unlock.techidaily.com/how-to-unlock-stolen-apple-iphone-12-in-different-conditionsin-drfone-by-drfone-ios/"><u>How To Unlock Stolen Apple iPhone 12 In Different Conditionsin | Dr.fone</u></a></li>
<li><a href="https://android-pokemon-go.techidaily.com/in-2024-catchemall-celebrate-national-pokemon-day-with-virtual-location-on-oppo-a1-5g-drfone-by-drfone-virtual-android/"><u>In 2024, CatchEmAll Celebrate National Pokémon Day with Virtual Location On Oppo A1 5G | Dr.fone</u></a></li>
<li><a href="https://hardware-tips.techidaily.com/intel-reveals-fix-for-persistent-cpu-stability-issues-overvolting-identified-as-primary-fault/"><u>Intel Reveals Fix for Persistent CPU Stability Issues: Overvolting Identified as Primary Fault</u></a></li>
<li><a href="https://tiktok-video-files.techidaily.com/mastering-video-storage-of-snapchat-stories/"><u>Mastering Video Storage of Snapchat Stories</u></a></li>
<li><a href="https://win-best.techidaily.com/resolution-rapide-comment-repartir-de-lattelee-avec-google-chrome-sur-windows-10/"><u>Résolution Rapide : Comment Repartir De L'Attelée Avec Google Chrome Sur Windows 10?</u></a></li>
<li><a href="https://win-best.techidaily.com/step-by-step-guide-securely-transferring-a-vmware-snapshot-to-a-new-virtual-machine/"><u>Step-by-Step Guide: Securely Transferring a VMware Snapshot to a New Virtual Machine</u></a></li>
<li><a href="https://win-manuals.techidaily.com/windows-1011programdata/"><u>Windows 10/11でProgramDataフォルダにアクセスする方法</u></a></li>
<li><a href="https://win-best.techidaily.com/1728494547434-windows-11/"><u>Windows 11上的最佳磁区修复软件 - 选型及其功效分析</u></a></li>
</ul></div>

<!-- affiliate ads begin -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/aYH0B2HqcIM?si=3fkoG85L6hAeB4ok" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<!-- affiliate ads end -->

