Hi Friends,

Have you ever wanted to tidy up your MKV collection but never had the time or energy?
Remove unwanted tracks to save storage space? Or add external tracks to create a clean, neat collection?
If the answer is yes, you're in the right place!

I'm excited to share a batch script I created to remux MKV files: "SamA MKV Batch Script".
This script allows you to do all the following at the same time:

1) Remove/keep only audio and subtitle tracks using their IDs and Languages
2) Remove/keep only audio and subtitle tracks using their Names!
3) Add external audio and subtitle tracks

Filtering tracks using their Names is useful when the IDs are not consistent and
the Languages are missing or not unique, like with some commentary tracks.



------------------------------------EDITING INSTRUCTIONS------------------------------------

1) Replace "D:\MKVToolNix 99.0 x64\mkvmerge.exe" with your mkvmerge path

2) • Delete or replace "1,2,eng" with the Track IDs and Languages
     you want to remove/keep only (separated by a Comma ,)
   • Comma , here means "And". "1,2,eng" means "Track IDs/Languages: 1 And 2 And eng"
   • Do the same for the Subs

3) • Delete or replace "Good_Audio¤Great_Audio¤Epic_Audio" with the Track Names
     you want to remove/keep only (separated by a Currency Sign ¤)
   • Currency Sign ¤ here means "And". "Good_Audio¤Great_Audio¤Epic_Audio" means
     "Track Names: Good_Audio And Great_Audio And Epic_Audio"
   • Do the same for the Subs

4) • Replace "MUXED_%~n1.mkv" with the new mkv filename pattern
   • MUXED_ here is a prefix. You can also add a suffix like %~n1_NEW.mkv

5) • Replace "%~n1*.ac3" with the filename pattern and extension of the external tracks you want to add
   • Delete or replace "jpn" with the Track Language you want
   • Delete or replace "Jpn_Audio" with the Track Name you want
   • Delete or replace "yes" with "no" for the Default Track flag
   • Do the same for the Subs

6) • Delete the Caret Exclamation ^! if you want to keep only the specified tracks (from Points 2 and 3 above)
   • Caret Exclamation ^! here means "Remove". ^!!FINAL_AUDIO! means "Remove the specified audio tracks".
     !FINAL_AUDIO! means "keep only the specified audio tracks"
   • Do the same for the Subs


• To Remove All Audio Tracks:

  Replace the value of FINAL_AUDIO on both lines with "-A". So it becomes...

  :FINAL_FLAGS
  if defined FINAL_AUDIO set "FINAL_AUDIO=-A"
  if not defined FINAL_AUDIO set "FINAL_AUDIO=-A"


• To Remove All Subs Tracks:

  Replace the value of FINAL_SUBS on both lines with "-S". So it becomes...
   
  if defined FINAL_SUBS set "FINAL_SUBS=-S"
  if not defined FINAL_SUBS set "FINAL_SUBS=-S"



------------------------------------USE INSTRUCTIONS------------------------------------

1) You need to have MKVToolNix as the script uses mkvmerge
2) Place the batch file inside the folder containing your MKV files
3) Open the file to run the script
4) • IMPORTANT: Check the "REM FOR FULL MATCHES, REPLACE LINE ABOVE WITH..."
     parts for full Track Name matching
   • If left unchanged, "Comm" (or any other part of "Commentary") will match Track Name "Commentary"
   • If replaced, only "Commentary" will match Track Name "Commentary"
5) External Tracks to be added must be in the same folder as your MKV files and must start with
   the same filename. For example: Episode01.mkv, then Episode01.ac3 and Episode01_Subs01.ass
6) Avoid editing anything else unless you know what you're doing
7) Always test the new MKV files before deleting the originals



------------------------------------FINAL NOTES------------------------------------

1) The script should work reliably with most MKV files. The only requirements are:
   • The mkvmerge JSON structure remains consistent across MKVToolNix versions.
     If the JSON structure changes in a future version, the parsing logic may need to be updated
   • The Currency Sign ¤ (which is extremely rare) is not used in Track Names.
     If it is used, simply change the delimiter to another rare character
2) The !MKVMERGE! command can be customized to add extra functions,
   like track ordering, chapter handling, and attachment support. For example:
   "!MKVMERGE!" -o "!NEW_FILE!" !FINAL_AUDIO! !FINAL_SUBS! "%~1" !ADD_AUDIO! !ADD_SUBS! --track-order 0:2,0:1
3) Feel free to share or modify the script
