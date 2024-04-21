# Environment Messages
## State
this message contains 3 property:

- ```agent_type```: Indicates the type of the connected agent whether it is player, coach, or trainer. The value can be ```PlayerT```, ```CoachT```, and ```TrainerT``` that shows. 
- ```world_model```: contains the information of the field environment that the agent recevied from the RCSSServer and parsed by the helios-base. More information is provided in the [WorldModel](#WorldModel) section. 
- ```full_world_model```: contains the information of the field environment that the agent recevied from the RCSSServer and parsed by the helios-base. More information is provided in the [WorldModel](#WorldModel) section.  

the difference between ```world_model``` and the ```full_world_model``` is that the ```full_world_model``` contains the information of all the objects in the field, while the ```world_model``` contains the information of the objects that are in the agent's view. Note that the ```world_model``` information is noisy and may not be accurate while the ```full_world_model``` is accurate.

In the defualt config of the RCSSServer, the agent only recieves the ```world_model``` information; however, by changing the config file, the agent can recieve the ```full_world_model``` information too. Although the agent revieves the ```full_world_model``` information, the full state data will be stored in the ```world_model``` property. To recieve both ```world_model``` and ```full_world_model``` information, the agent should change the ```player.conf``` file in the proxy base. 
```
TODO the property of the player.conf for recieving the full_world_model
```

### WorldModel
The ```WorldModel``` type contains the following information:
- ```intercept_table```: Contains the data of the important players that can intercept the ball.In [here](#InterceptTable) we explain more about this data. 
- ```our_team_name```: The name of the team that the agent is playing for.
- ```their_team_name```: The name of the opponent team.
- ```our_side```: The side of the field that the agent is playing for. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN```.
- ```last_set_play_start_time```: The time that the last set play (Game Type) started. 
- ```self```: The information of the agent itself, such as the uniform number, the position, the velocity, etc. In the [Self](#Self) section, we explain more about this data.
- ```ball```: The information of the ball, such as the position, the velocity, etc. In the [Ball](#Ball) section, we explain more about this data.
- ```teammates```*: This property is a list of the ```Players``` that contains the information of the teammates. In the [Player](#Player) section, we explain more about this data.
- ```opponents```*: This property is a list of the ```Players``` that contains the information of the opponents. In the [Player](#Player) section, we explain more about this data.
- ```unknowns```: This property is a list of the ```Players``` that contains the information of the unknown players. Unknown players are the ones that the agent did not receive any information about the uniform number and the side of them. In the [Player](#Player) section, we explain more about this data.
- ```our_players_dict```*: This property is a dictionary that contains the information of the teammates. The key of the dictionary is the uniform number of the player. Note that if the agent does not have any data about a player, the player will not be in the dictionary (check for the null). In the [Player](#Player) section, we explain more about this data.
- ```their_players_dict```*: This property is a dictionary that contains the information of the opponents. The key of the dictionary is the uniform number of the player. Note that if the agent does not have any data about a player, the player will not be in the dictionary (check for the null). In the [Player](#Player) section, we explain more about this data.
- ```our_goalie_uniform_number```: The uniform number of the goalie of the agent's team.
- ```their_goalie_uniform_number```: The uniform number of the goalie of the opponent's team.
- ```offside_line_x```: The x position of the offside line.
- ```ofside_line_x_count```: The number of cycles that passed of the offside line calculation.
- ```kickable_teammate_id```: The uniform number of the teammate that the agent can kick the ball to.
- ```kickable_opponent_id```: The uniform number of the opponent that the agent can kick the ball to.
- ```last_kick_side```: The side that the last kick was done. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN```.
- ```last_kicker_uniform_number```: The uniform number of the player that kicked the ball last time.
- ```cycle```: The current cycle of the game.
- ```stoped_cycle```: The cycle that the game stopped. The stopped cycle increase when the game cycle is not updated. This happens when the games stops for some game modes.
- ```game_mode_type```: The current mode of the game. This value can be ```PlayOn```, ```BeforeKickOff```, etc. We will explain more about this in the [GameModeType](#GameModeType) section.
- ```left_team_score```: The score of the left team.
- ```right_team_score```: The score of the right team.
- ```is_our_set_play```: Indicates whether the agent's team is in the set play mode. It means if the agent's team should kick the ball for the current game mode.
- ```is_their_set_play```: Indicates whether the opponent's team is in the set play mode. It means if the opponent's team should kick the ball for the current game mode.
- ```our_team_score```: The score of the agent's team.
- ```their_team_score```: The score of the opponent's team.
- ```is_penalty_kick_mode```: Indicates whether the game is in the penalty kick mode.
- ```helios_home_positions```: The position of the players based on the defined formations in the ```src/formtaions-dt``` directory. The position of the players is calculated based on the position of the ball and the formation of the team. This position is calculated by the base and is stored in this dictionary. The key of the dictionary is the uniform number of the player and the value is the position of the player.

*: TODO

#### InterceptTable
The ```InterceptTable``` type contains the following information:
- ```self_reach_steps```: The number of cycles that the agent can reach the ball.
- ```first_teammate_reach_steps```: The number of cycles that the first teammate can reach the ball. Note that the agent is not considered as a teammate.
- ```second_teammate_reach_steps```: The number of cycles that the second teammate can reach the ball. Note that the agent is not considered as a teammate.
- ```first_opponent_reach_steps```: The number of cycles that the first opponent can reach the ball.
- ```second_opponent_reach_steps```: The number of cycles that the second opponent can reach the ball.
- ```first_teammate_id```: The uniform number of the first teammate that can intercept the ball.
- ```second_teammate_id```: The uniform number of the second teammate that can intercept the ball.
- ```first_opponent_id```: The uniform number of the first opponent that can intercept the ball.
- ```second_opponent_id```: The uniform number of the second opponent that can intercept the ball.
- ```self_intercept_info```: TODO?!

#### Self
The ```Self``` type contains the following information:
- ```position```: The position of the agent.
- ```seen_position```: The position of the agent that the agent saw.
- ```heard_position```: The position of the agent that the agent heard.
- ```velocity```: The velocity of the agent.
- ```seen_velocity```: The velocity of the agent that the agent saw.
- ```pos_count```: The number of cycles that passed since the agent's position was updated.
- ```seen_pos_count```: The number of cycles that passed since the agent's seen position was updated. TODO ?!(Correct?)
- ```heard_pos_count```: The number of cycles that passed since the agent's heard position was updated. TODO ?!(Correct?)
- ```vel_count```: The number of cycles that passed since the agent's velocity was updated.
- ```seen_vel_count```: The number of cycles that passed since the agent's seen velocity was updated. TODO ?!(Correct?)
- ```ghost_count```: TODO ?!
- ```id```: TODO?!
- ```side```: The side of the agent. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN``.
- ```uniform_number```: The uniform number of the agent.
- ```uniform_number_count```: The number of cycles that passed since the agent's uniform number was updated.
- ```is_goalie```: Indicates whether the agent is the goalie of the team.
- ```body_direction```: The direction of the agent's body.
- ```body_direction_count```: The number of cycles that passed since the agent's body direction was updated.
- ```face_direction```: The direction of the agent's face. This value is the direction that the agent is looking at and it is global, not relative to the player's body.
- ```face_direction_count```: The number of cycles that passed since the agent's face direction was updated.
- ```point_to_direction```: The direction that the agent is pointing to. Check the [PointToDirection](#PointToDirection) section for more information.
- ```point_to_direction_count```: The number of cycles that passed since the agent's point to direction was updated.
- ```is_kicking```: Indicates whether the agent is kicking the ball.
- ```dist_from_ball```: The distance of the agent from the ball.
- ```angle_from_ball```: The angle of the agent from the ball. This value is relative to the agent's body. (TODO CHECK)
- ```ball_reach_steps```: The number of cycles that the agent can reach the ball.
- ```is_tackling```: Indicates whether the agent is tackling.
- ```relative_neck_direction```: The direction of the agent's neck relative to the agent's body. It's the value of the face direction relative to the body direction.
- ```stamina```: The stamina of the agent.
- ```is_kickable```: Indicates whether the agent can kick the ball.
- ```catch_probability```: The probability of the agent to catch the ball. Catching the ball is for the goalie.
- ```tackle_probability```: The probability of the agent to tackle the opponent. (TODO CHECK)
- ```foul_probability```: The probability of the agent to foul the opponent while tackling. (TODO CHECK)
- ```view_width```: The width of the agent's view. This value can be ```NARROW```, ```NORMAL```, or ```WIDE``.
- ```type_id```: The player type id of the agent. This value is explained in the [PlayerType](#PlayerType) section.
- ```kick_rate```: The rate of the agent to kick the ball. This value is calculated based on the player type and the position of the ball relative to the agent's position and body.

#### Player
The ```Player``` type contains the following information:
- ```position```: The position of the player.
- ```seen_position```: The position of the player that the agent saw.
- ```heard_position```: The position of the player that the agent heard.
- ```velocity```: The velocity of the player.
- ```seen_velocity```: The velocity of the player that the agent saw.
- ```pos_count```: The number of cycles that passed since the player's position was updated.
- ```seen_pos_count```: The number of cycles that passed since the player's seen position was updated. TODO ?!(Correct?)
- ```heard_pos_count```: The number of cycles that passed since the player's heard position was updated. TODO ?!(Correct?)
- ```vel_count```: The number of cycles that passed since the player's velocity was updated.
- ```seen_vel_count```: The number of cycles that passed since the player's seen velocity was updated. TODO ?!(Correct?)
- ```ghost_count```: TODO ?!
- ```dist_from_self```: The distance of the player from the agent.
- ```angle_from_self```: The angle of the player from the agent. This value is relative to the agent's body. (TODO CHECK)
- ```id```: TODO?!
- ```side```: The side of the player. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN``.
- ```uniform_number```: The uniform number of the player.
- ```uniform_number_count```: The number of cycles that passed since the player's uniform number was updated.
- ```is_goalie```: Indicates whether the player is the goalie of the team.
- ```body_direction```: The direction of the player's body.
- ```body_direction_count```: The number of cycles that passed since the player's body direction was updated.
- ```face_direction```: The direction of the player's face. This value is the direction that the player is looking at and it is global, not relative to the player's body.
- ```face_direction_count```: The number of cycles that passed since the player's face direction was updated.
- ```point_to_direction```: The direction that the player is pointing to. Check the [PointToDirection](#PointToDirection) section for more information.
- ```point_to_direction_count```: The number of cycles that passed since the player's point to direction was updated.
- ```is_kicking```: Indicates whether the player is kicking the ball.
- ```dist_from_ball```: The distance of the player from the ball.
- ```angle_from_ball```: The angle of the player from the ball. This value is relative to the player's body. (TODO CHECK)
- ```ball_reach_steps```: The number of cycles that the player can reach the ball.
- ```is_tackling```: Indicates whether the player is tackling.
- ```type_id```: The player type id of the player. This value is explained in the [PlayerType](#PlayerType) section.

#### GameModeType
The ```GameModeType``` is an enum that contains the following values:
- ```BeforeKickOff```: The game mode that the game is before the kick-off.
- ```TimeOver```: The game mode that the time is over. (TODO CHECK)
- ```PlayOn```: The game mode that the game is playing.
- ```KickOff_```: The game mode that the game is in the kick-off mode.
- ```KickIn_```: The game mode that the game is in the kick-in mode.
- ```FreeKick_```: The game mode that the game is in the free-kick mode.
- ```CornerKick_```: The game mode that the game is in the corner-kick mode.
- ```GoalKick_```: The game mode that the game is in the goal-kick mode. (TODO CHECK?)
- ```AfterGoal_```: The game mode that the game is after the goal.
- ```OffSide_```: The game mode that the game is in the offside mode.
- ```PenaltyKick_```: The game mode that the game is in the penalty-kick mode.
- ```FirstHalfOver```: The game mode that the first half is over.
- ```Pause```: The game mode that the game is paused. (TODO CHECK)
- ```Human```: The game mode that the game is in the human mode. (TODO CHECK)
- ```FoulCharge_```: The game mode that the game is in the foul-charge mode.
- ```FoulPush_``` TODO
- ```FoulMultipleAttacker_```
- ```FoulBallOut_```
- ```BackPass_```
- ```FreeKickFault_```
- ```CatchFault_```
- ```IndFreeKick_```
- ```PenaltySetup_```
- ```PenaltyReady_```
- ```PenaltyTaken_```
- ```PenaltyMiss_```
- ```PenaltyScore_```
- ```IllegalDefense_```
- ```PenaltyOnfield_```
- ```PenaltyFoul_```
- ```GoalieCatch_```
- ```ExtendHalf```
- ```MODE_MAX```


# Agent Actions
After receiving the State message, the agent should send a list of actions to the base so the base can execute them and send them to the RCSSServer. The ```PlayerActions``` message contains a list of [```Action```](#Action). 

This list should only contains one Body Action and several other actions. By Body Action, we mean the actions that are related to the agent's body, such as ```Dash```, ```Turn```, ```Kick```, ```Tackle```, ```Catch```, and ```Move```. The agent can only do these actions once in a cycle. The other actions, such as ```TurnNeck```, ```ChangeView```, ```Say```, ```PointTo```, and ```AttentionTo``` can be done multiple times in a cycle. The agent can only do each type of action once in a cycle. For example, the agent can only do one ```Dash``` action in a cycle, while it can ```ChangeView```, ```Say```, and ```TurnNeck``` in that cycle. Note that the agent cannot do the second type actions more than once in a cycle.

In addition to that, the agent can send the some debug actions to the base. These actions are ```Log``` and ```DebugClient```. These actions are useful when you are using the [soccerwindow2](https://github.com/helios-base/soccerwindow2) as the monitor. These actions are for the debug tools of this application.

## Low-Level Actions
## High-Level Actions

## Action
The action contains only one action; however, this action can be one of the following actions:

- ```Dash```
- ```Turn```
- ```Kick```
- ```Tackle```
- ```Catch```
- ```Move```
- ```TurnNeck```
- ```ChangeView```
- ```Say```
- ```PointTo```
- ```PointToOf```
- ```AttentionTo```
- ```AttentionToOf```
- ```Log```
- ```DebugClient```
- ```Body_GoToPoint```
- ```Body_SmartKick```
- ```Bhv_BeforeKickOff```
- ```Bhv_BodyNeckToBall```
- ```Bhv_BodyNeckToPoint```
- ```Bhv_Emergency```
- ```Bhv_GoToPointLookBall```
- ```Bhv_NeckBodyToBall```
- ```Bhv_NeckBodyToPoint```
- ```Bhv_ScanField```
- ```Body_AdvanceBall```
- ```Body_ClearBall```
- ```Body_Dribble```
- ```Body_GoToPointDodge```
- ```Body_HoldBall```
- ```Body_Intercept```
- ```Body_KickOneStep```
- ```Body_StopBall```
- ```Body_StopDash```
- ```Body_TackleToPoint```
- ```Body_TurnToAngle```
- ```Body_TurnToBall```
- ```Body_TurnToPoint```
- ```Focus_MoveToPoint```
- ```Focus_Reset```
- ```Neck_ScanField```
- ```Neck_ScanPlayers```
- ```Neck_TurnToBallAndPlayer```
- ```Neck_TurnToBallOrScan```
- ```Neck_TurnToBall```
- ```Neck_TurnToGoalieOrScan```
- ```Neck_TurnToLowConfTeammate```
- ```Neck_TurnToPlayerOrScan```
- ```Neck_TurnToPoint```
- ```Neck_TurnToRelative```
- ```View_ChangeWidth```
- ```View_Normal```
- ```View_Synch```
- ```View_Wide```
- ```HeliosGoalie```
- ```HeliosGoalieMove```
- ```HeliosGoalieKick```
- ```HeliosShoot```
- ```HeliosChainAction```
- ```HeliosBasicOffensive```
- ```HeliosBasicMove```
- ```HeliosSetPlay```
- ```HeliosPenalty```
- ```HeliosCommunicaion```
