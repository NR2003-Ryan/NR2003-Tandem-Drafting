README V 0.1


NR2003 Tandem Drafting mod by NR2003_Ryan
https://www.reddit.com/user/NR2003_Ryan


This mod aims to replicate 2011 style super speedway racing with 2 car tandems.


It is a work in progress, and due to game limitations, it’s more of a mix between pack racing and tandem drafting.
It’s also hard to race with both humans and ai together.


Feel free to modify, redistribute, and publish as your own. I don’t care!





**How to install**


First, it is recommended to install in a separate version of NR 2003. An easy way to do this is to copy and paste your NASCAR Racing 2003 Season folder, rename, and use the copy.


1. Download the NR2003_TDraft_Cup11ss.exe from this project and place it in your NASCAR Racing 2003 Season folder, or the copy that you made. When you start the game, make sure to run this .exe.


    If you only want to race with humans, you are done! The rest is for racing with ai.


2. Download the papy_ai.ini from this project and place it in your NASCAR Racing 2003 Season folder, or the copy you made. Replace the existing file. (You might want to back up the original if you are only using one NR2003 installation)


3. Download the DMR Cup 11 SS mod: https://stunodracing.net/index.php?resources/dmrcup11ss.1039/, or you can find it here: https://nr2k3.weebly.com/mods.html . You can use other mods and carsets, but it will likely require some tweaking. Extract and place the Cup11ss folder in your NASCAR Racing 2003 Season\series folder.


4. Set up the track(s) that you want to use. Currently there are 3 supported tracks, but you can tweak it to work on other tracks. See “Want to make your own version?” section below.


    Daytona 2011: Download the track: https://www.drnoisepaints.com/tracks/revampedreloaded/Daytona_Revamped_2011b.7z or find “Daytona_Revamped_2011b” from here: https://nr2k3.weebly.com/superspeedways.html . Extract it and run the .exe installing it into your NASCAR Racing 2003 Season\tracks folder. Then, go to the “Daytona_Revamped_2011b” folder in this project and copy and paste all of the files into NASCAR Racing 2003 Season\tracks\Daytona_Revamped_2011b and replace existing files.


   Eight Bowl: Download the track: http://www.mediafire.com/download/y3wzmz5ynzt/eight_bowl.exe or find it here: https://docs.google.com/spreadsheets/d/1RBBIzRon8LnMU4BKSaKx7CGbDl_W-r1YkYep9l5kDok/htmlview . Run the .exe installing it into your NASCAR Racing 2003 Season\tracks folder. Then, go to the “eight_bowl” folder in this project and copy and paste all of the files into NASCAR Racing 2003 Season\tracks\eight_bowl and replace existing files.


    Talladega 2010: Download the track: https://www.drnoisepaints.com/tracks/revampedreloaded/Talladega_revamped_2010.7z or find it here: https://nr2k3.weebly.com/superspeedways.html . Run the .exe installing it into your NASCAR Racing 2003 Season\tracks folder. Then, go to the “Talladega_revamped_2010” folder in this project and copy and paste all of the files into NASCAR Racing 2003 Season\tracks\Talladega_revamped_2010 and replace existing files.


5. Modify the Car Ratings for Cup11ss (Not strictly necessary, but it helps):
    Reduce the Aggression for all drivers down to 0 (for both min and max). You can do this in game in the opponent manager, or the much easier way to do it is through NRatings https://github.com/64Soft/NRatings.Client .


    Adjust the Finishing and Qualifying ratings to min: 0 and max: 100 for all cars.


    [Optional]: if you want to go the extra mile, you can boost backmarker cars’ Finishing and Qualifying ratings and lower frontrunners’. The purpose of adjusting these 2 ratings is to get a rotation of leading cars throughout the race.


6. Enjoy! Make sure to run the NR2003_TDraft_Cup11ss.exe when you play with this mod, and use the cup11ss series. When you set up the race, turn Damage OFF.




**Want to make your own version?**


Here's how this mod works under the hood:


1. Modified .exe


    This is where the physics magic happens. Everything else besides the .exe is just controlling ai behavior.


    Creating your own .exe might be simpler than you think! https://www.reddit.com/r/Nr2003/comments/4eag6i/nr2003_physics_editor_tutorial/


    The modified .exe in this project contains 3 simple edits:


    1. Drag is increased to 0.50 (line 43)
       
    &H2C7D2,Sing,0.50,0.406081,??? Drag,Chassis,cup-1,43
    
    
    3. Drafting strength is increased to 7 (line 53)
       
    &H2C924,Sing,7,1,???,Chassis,cup-1,53
    
    
    5. Drafting distance is decreased to 0.2 (line 54)
       
    &H2C92E,Sing,0.2,1,???,Chassis,cup-1,54
    
    
    Increasing drafting strength while lowering distance makes locking bumpers and pushing really strong, while pack racing feels kinda similar to normal. A side effect is this also increases side drafting strength a ton.
    
    
    Drag is increased simply to reduce speeds down to reasonable levels. An alternative way to do this is modifying the engine. For example, you can decrease Torque-2 and Torque-3 to achieve a similar result.


2. Modified papi_ai.ini


    The papi_ai.ini controls numerous parameters of ai behavior and physics
    
    
    The most important piece to modify is the yaw_accel_k1 and k2. These two params are increased to 1.0, which makes the ai nearly impossible to spin.
    
    
    The next piece is increasing the driver consistency so that the ai run smoother lines and in theory, stay in line better. In practice, the difference is hard to notice.
    
    
    driver_consistency is increased to 1.0. Others are decreased to near 0, which actually increases consistency.
    
    
    A couple of fields in [ behavior ] are modified too to give the ai godlike spin recovery. These aren't necessary if you are using the yaw_accel_* parameters. But keeping these crashing_recovery parameters high helps if you want to decrease the yaw_accel.


3. Modified car ratings


    Aggression is set to zero to get the AI to stay in line with the car in front more often rather than constantly trying to pass.
    
    
    Consistency is covered by the papy_ai.ini
    
    
    Cars have the max range [0,100] for qualifying and finishing ratings in order to promote a rotation of front runners throughout the race, similar to SS racing in 2011ish. For example, a car might have poor qualifying and start in the back, but great finishing and finish near the front.


4. track.ini


    The core piece of the track.ini that makes this work is setting ai_drafting_distance to < 1. The drafting distance is in car lengths, where 1.0 means that the cars will be bumper to bumper. In order to get them to bump harder and push, it’s set to < 1.
    
    
    The rest is all pack management. With default track.ini settings, the cars will form massive 5 wide wads. While they do lock bumpers and push, a ginormous cluster isn’t what we are looking for in a tandem drafting mod.
    
    
    To fix this, ai_grip_modifier is reduced and typically the outer lane grip is increased (track_paint_grip for most tracks). Then, ai_line_modifier is reduced to make the ai on the inside lane check up just slightly on the corners if there are cars to their outside. This both creates multigroove racing and helps disperse the pack. The effect gets stronger as tires wear.
    
    
    A second alternative strategy to the above is to actually increase ai_line_modifer while reducing the grip on the inside lane to cause weaker cars to slide up the track. If the numbers are tweaked just right, both of these strategies can be used, but most tracks just the first strategy above.
    
    
    Additionally, ai_dlat_pad is increased usually to about 2. This spreads the cars out more laterally, which helps disperse packs.
    
    
    Lastly, if you have done all the above, the big packs will eventually disperse. But you start with a big wad for the first 5-8 laps or so. To fix this, ai_pacing_distance and ai_bunching_distance are increased to about 4. This spreads the cars out on starts and restarts so they don’t start in a big wad.


5. .lp files


    The .lp files dictate the racing line the AI follows.
    
    
    There's 3 lines that impact the AI behavior with regards to tandem drafting.
    
    
    race.lp is the ideal racing line
    
    
    maxrace.lp and minrace.lp are the inner and outer boundaries of the track that the AI won't cross.
    
    
    I'll explain the science below:
    
    
    First and foremost, cars stay hooked together better if they are traveling along the edge of the track boundaries. Thus, the ideal racing line (race.lp) is designed to run almost entirely along the boundaries, which isn't too far off from the original race.lp’s.
    
    
    The reason the AI stay hooked together better is kinda hard to explain. But basically, a 2 car tandem inside a wad of cars is less likely to have each car veer a different direction if they are along the edge, because they have nowhere to go.
    
    
    Secondly, the outer track boundary (minrace.lp) is often bumped inward a little to keep cars off the wall.
    
    
    Lastly, the .lp files can help with pack management. For example, Eight Bowl had an issue with having 8+ car single file freight trains that never make a pass. Moving the ideal line to the top on turn 3 and 4 created an opportunity for cars to dive inside and pass, so it fixed that issue.
