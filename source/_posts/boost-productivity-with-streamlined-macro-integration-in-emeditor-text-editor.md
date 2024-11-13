---
title: Boost Productivity with Streamlined Macro Integration in EmEditor Text Editor
date: 2024-11-06T03:25:05.818Z
updated: 2024-11-12T19:33:25.558Z
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
<li><a href="https://screen-activity-recording.techidaily.com/new-in-2024-step-by-step-tutorial-for-efficient-video-capturing-via-zd/"><u>[New] In 2024, Step-by-Step Tutorial for Efficient Video Capturing via ZD</u></a></li>
<li><a href="https://fox-http.techidaily.com/updated-zip-archive-handling-for-srt-output-generation/"><u>[Updated] Zip Archive Handling for SRT Output Generation</u></a></li>
<li><a href="https://discover-blog.techidaily.com/abbyy-laut-top-rated-in-the-2024-idp-peak-matrix-evaluation-by-everest-group/"><u>ABBYY Laut: Top-Rated in the 2024 IDP Peak Matrix Evaluation by Everest Group</u></a></li>
<li><a href="https://win-best.techidaily.com/behebe-das-xcopy-verzeichnisnicht-erstellen-problem-mit-diesen-drei-strategien/"><u>Behebe Das 'XCopy-Verzeichnisnicht Erstellen'-Problem Mit Diesen Drei Strategien</u></a></li>
<li><a href="https://buynow-reviews.techidaily.com/breaking-down-the-performance-of-audews-compact-trustworthy-portable-air-compressor/"><u>Breaking Down the Performance of Audew’s Compact, Trustworthy Portable Air Compressor</u></a></li>
<li><a href="https://win-best.techidaily.com/data-restoration-techniques-how-to-reclaim-deleted-files-on-your-hard-disk/"><u>Data Restoration Techniques: How to Reclaim Deleted Files on Your Hard Disk</u></a></li>
<li><a href="https://extra-lessons.techidaily.com/essential-guide-to-os-independent-media-software/"><u>Essential Guide to OS-Independent Media Software</u></a></li>
<li><a href="https://screen-mirror.techidaily.com/in-2024-how-screen-mirroring-apple-iphone-13-mini-to-tv-or-pc-drfone-by-drfone-ios/"><u>In 2024, How Screen Mirroring Apple iPhone 13 mini to TV or PC? | Dr.fone</u></a></li>
<li><a href="https://win-best.techidaily.com/la-selection-de-votre-futur-guide-complet-pour-trouver-le-meilleur-ssd-interne-en-2024/"><u>La Sélection De Votre Futur: Guide Complet Pour Trouver Le Meilleur SSD Interne en 2024</u></a></li>
<li><a href="https://ai-video-editing.techidaily.com/1713964617797-new-read-and-learn-how-to-convert-a-slow-motion-video-to-normal-in-this-guide-besides-find-the-best-desktop-solution-to-adjust-video-speed-quickly-and-easil/"><u>New Read and Learn How to Convert a Slow-Motion Video to Normal in This Guide. Besides, Find the Best Desktop Solution to Adjust Video Speed Quickly and Easily for 2024</u></a></li>
<li><a href="https://win-best.techidaily.com/step-by-step-guide-to-retrieving-trashed-documents-on-windows-easily-post-empty-recycle-bin/"><u>Step-by-Step Guide to Retrieving Trashed Documents on Windows Easily Post-Empty Recycle Bin</u></a></li>
</ul></div>

<!-- affiliate ads begin -->
<a href="https://aligracehair.sjv.io/c/5597632/2016143/19272" target="_top" id="2016143">
  <img src="//a.impactradius-go.com/display-ad/19272-2016143" border="0" alt="https://techidaily.com" width="300" height="90"/>
</a>
<img height="0" width="0" src="https://aligracehair.sjv.io/i/5597632/2016143/19272" style="position:absolute;visibility:hidden;" border="0" />
<!-- affiliate ads end -->

