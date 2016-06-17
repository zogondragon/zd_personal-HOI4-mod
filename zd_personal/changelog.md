# R4 - 2016-06-17
* In /common/defines/
  - In '00_graphics.lua', many graphic variables exist.
* In /common/idea_tags/
  - government, research/production teams, military staffs hiring value.
* In /common/ideas/
  - Various laws and national spirits resides in here.
  - Political advisors are in [nation name].txt.
  - `allowed` condition is for FRA tag. `allowed_civil_war` is for civil war
  situation. Does every civil war country receive certain national spirits?
  - Manufacturers are also in [nation name].txt.
* In /common/ideologies/
  - In '00_ideologies.txt', there are many sub-ideologies for democratic,
  fascist, and communist. Dynamic faction names and sub-ideologies means future
  DLC will expand upon internal / external politics.
  - `ai_democratic`. Interesting.
* In /common/names/
  - In '00_names.txt', name generation happens here.
* In /common/national_focus/
  - `hidden_effect` seems fun.
* In /common/scripted_triggers/
  - This file can serve as macros for readability. Complex triggers can be
  defined here and modders can use it by calling it.
* In /common/technologies/
  - `ai_research_weights` used for weighting certain unit types for AI research.
  - Technology tags are in '00_technology.txt'.
  -
* In /common/timed_activities/
  - There is only one file: '00_stage_coup.txt'.
* In /common/unit_leader/
  - Naval leader skill progression is weird. `naval_hit_chance` is linearly
  increased per skill level, but `naval_coordination` is different for 1~5 skills
  and 6~9 skills. I don't think there is a significant difference between
  linear progression and current piecewise linear progression. So I modifed this.
  - In '00_traits.txt', `ranger` trait gains xp from `is_fighting_in_terrain=hills`
  and `is_fighting_in_terrain=forest`, but only gains combat modifier for forest.
  Also, there is already a trait called `hill_fighter`. So gaining hills xp for
  ranger trait is quite redundant. Possible bug?
  - `bearer_of_artillery` is disabled. Why?
  - `blockade_runner` is not gainable. Why?
* In /common/units/
  - Battlecruiser, rather than Battle Cruiser.
  - __TYPO:__ in '00_names.txt': Mountaineer Division instead of Mounaineer
  Division.
* AI improvement plan
  - __TODO:__ AI strategic redeployment behavior is a real mess. Temporarily
  disabling it or making the minimum range for strategic redeployment is my
  solution until 1.10 patch.
    - (do something)


# R3 - 2016-06-16
* In /common/defines/
  - In '00_defines.lua', there are many global constants for gaming.
  - `MAJOR_IC_RATIO` is interesting. Major nations are not designated by devs
  but dynamically calculated by using IC ratio?
  - `COMBAT_VALUE_ORG_IMPORTANCE` need to be more larger than
  `COMBAT_VALUE_STR_IMPORTANCE` I think. Because almost every time a division
  loses combat because of ORG damage, not STR damage.
  - General skill advantage 1 is worth recon advantage 5. This is additional
  beside of attack/defense bonus 5% per skill level.
  - Regiment, brigade, battalions are all mixed in the game files. They seriously
  need to be consistent.
  - `UNIT_DIGIN_CAP`, `UNIT_DIGIN_SPEED` are related to entrenchment.
  - __TYPO__: `IS_AMPHIBIOUS_LIMNIT` should be `IS_AMPHIBIOUS_LIMIT`.
* Land warfare balancing plan
  - ART: in the vanilla, ART battalions are God. I will reduce the offensive
  effectiveness of ART especially for the early game. Also, ART divisions should
  have lower movement speed compared to INF divisions, because ART is heavy
  equipment. However, with ample research and upgrades ART and R-ART should be
  a force to be reckoned with.
    - __TODO:__ Artillery land movement decreased from 4.0kph to 3.6kph.
    - __TODO:__ Artillery equipment soft attack decreased from x to y.
  - INF: AI tend to use pure INF divisions, so a little buff to INF can be good
  for single player experience.
    - __TODO:__ Infantry soft attack increased from x to y.
  - Planning bonus and entrenchment: especially for Grand Battleplan doctrine,
  max planning bonus is insanely strong. +100% attack for almost 100 days is
  just insane. It can cancel out almost every defensive position. The reason
  that AI is weak at defense is the player planning bonus advantage. On the other
  hand, entrenchment is not scaling well to the progress of land doctrines.
    - `PLANNING_MAX` reduced from 0.5 to 0.3.
    - __TODO:__ Max entrenchment bonuses are assigned to various land doctrine techs.
* Air warfare balancing plan
  - NAV: Naval Strike mission and Port Strike mission are ridiculously effective
  against ships, both combat impact and IC impact wise.
    - `COMBAT_MAX_WINGS_AT_ONCE_PORT_STRIKE` reduced from 1000 to 6. In real
    life, port and harbor has some kind of protection against torpedos and
    dive bombs. 1000 NAV wings simultaneously striking anchored fleets is
    very very unrealistic.
    - `NAVAL_STRIKE_DAMAGE_TO_STR` decreased from 3.0 to 2.0.
    - `NAVAL_STRIKE_DAMAGE_TO_ORG` decreased from 3.0 to 2.0.
    - `NAVAL_STRIKE_DETECTION_BALANCE_FACTOR` decreased from 0.7 to 0.6. This
    factor change makes naval strike less frequent given a sea region.
  - CAS and TAC: Ground Support mission is vastly biased for IC heavy major
  nations with 1500++ bomber reserves. Limiting bomber wings at the same time
  can help minor nations to withstand the air inferiority.
    - `COMBAT_MAX_WINGS_AT_GROUND_ATTACK` reduced from 30 to 15.
    - `ANTI_AIR_PLANE_DAMAGE_CHANCE` increased from 0.1 to 0.2.
  - FTR and H-FTR: the loss of FTR and H-FTR is so hard that almost every
  player produces FTR and H-FTR with like 50++ factories. Compared to other
  type of airplanes this is too harsh. Especially FTR and H-FTR carry out
  Air Superiority mission very much, and this mission takes tolls from accidents
  quite frequently. We should reduce the loss of FTR and H-FTR for each air
  combat so the airfleet of inferior nation should not be eliminated completely.
    - `COMBAT_ATTACK_PASSES_AT_ONCE` reduced from 0.1 to 0.05.
* Naval warfare balancing plan
  - CV vs BB: CAS and NAV on carrier mission is generally too strong against
  non-CV fleets. Toning down Carrier Mission Efficiency of CAS and NAV a little
  bit should make naval battle more interesting.
    - `EXPERIENCE_FACTOR_NON_CARRIER_GAIN` increased from 0.05 to 0.07.
    - `EXPERIENCE_FACTOR_CARRIER_GAIN` decreased from 0.10 to 0.07.
    - `SHORE_BOMBARDMENT_CAP` increased from 0.25 to 0.5. This change will favor
    BB and SH-BB with increased utility for naval invasion.
  - Naval AA: CA and CL is known for their heavy AA equipment and they were
  used as anti-air escort mission for CV and BB. Improving naval AA efficiency
  make cruisers more viable choice. Currently DD rules the sea because they can
  slaughter SS and do fine against any other type of missions. Cruisers should
  have more edges to compete with DD.
    - `ANTI_AIR_TARGETTING_TO_CHANCE` increased from 0.07 to 0.10.
    - `ANTI_AIR_ATTACK_TO_AMOUNT` increased from 0.005 to 0.010.
    - `ANTI_AIR_TARGETTING` increased from 0.9 to 1.2.
  * AI improvement plan
    - AI XP usage is too irrelevant and too frequent at the moment.
      - `DIVISION_UPGRADE_MIN_XP` increased from 5 to 50.
      - `DIVISION_CREATE_MIN_XP` increased from 100 to 150.
      - `VARIANT_UPGRADE_MIN_XP` increased from 100 to 200.
    - `DIVISION_DESIGN_WEIGHTS` needs quite a tuning because almost every value
    is filled with 0s.
      - _hard_attack_ from 0.0 to 0.2.
      - _recon_ from 0.0 to 0.1.
      - _defense_ from 1.0 to 1.5.
      - _breakthrough_ from 1.0 to 1.5.
      - _navy-attack_ from 0.0 to 1.0.
      - _navy-fire_range_ from 0.0 to 0.5.
      - _navy-naval_range_ from 0.0 to 0.5.
      - _navy-carrier_size_ from 0.0 to 1.0.
      - _air-air_range_ from 0.0 to 2.0.
      - _air-air_agility_ from 0.0 to 1.0.
      - _armor_value_ from 1.0 to 2.0.
      - _ap_attack_ from 0.5 to 1.5.
    - Reevaluating bad combats are too scarce. 72 hours will be enough to find
    out.
      - `HOUR_BAD_COMBAT_REEVALUATE` decreased from 168 to 72.
# R2 - 2016-06-15
* In /common/ai_strategy/
  - In 'doctrines.txt': `unit_ratio` can affect the ratio of unit production.
  `-100` means -100%.
  - Given the file here, `ai_strategy` is a data set of integers consist of
  `unit_base` and `unit_ratio`. AI will probabilistically produce equipments and
  divisions.
  - Actually, cavalry has its military policing uses, so completely not producing
  CAV just because you can produce MOT is counter-productive. You definitely do
  not want your MOT to chase after partisans.
  - __TECH__ has `motorised_infantry`, but in every other instance it is
  `motorized`. Be careful when you mod this.
  - `grand_battle_plan_ratios`, mechanized? And `anti_tank` gets 20% boost,
  but `artillery` gets no boost? Strange.
  - I need access to `ai_strategy` item, to find out and hopefully expand it
  to have more `id`.
  - There is no FRA and USA files in /common/ai_strategy/. Maybe I can write
  some for test. FRA will be my AI experiment subject.
  - The first 11 lines of 'ENG.txt' is commented. I think it is a possible
  action list for `ai_strategy` in script engine. The actions are `befriend`,
  `conquer`, `antagonize`, `build_ship`, `build_army`, `unit_ratio`,
  `build_building`, `research_tech`, `garrison`, `protect`, `influence`.
  The exact behavior for each action is not determined yet.
  - Are `date > 1937.12.31` and `date > "1937.12.31"` same? Is this a bug or
  allowed syntax?
  - __BUG__ in 'GER.txt': `china_ally` item has following enable condition.
```shell
enable = {
        tag = GER
        #has_completed_focus = GER_japan_friend << BUG
        has_completed_focus = GER_china_friend
        country_exists = CHI
}
```  
* In /common/ai_templates/
  - In 'generic.txt': division templates are located here.
  - In division templates files, `artillery` means support battalion, and
  `artillery_brigade` means line artillery battalion.
  - I need to determine what `stat_weights` is doing.
  - The comment about regiments and support are inconsistent with file contents.
  Which one is right one? Possible __BUG__.
  - Nation specific templates such as 'templates_GER.txt' are blank, so I cannot
  infer the method here.
* In /common/countries/
  - 'D01.txt ~ D15.txt' files are for civil war countries. Dynamic tags are
  the root of all civil war bugs? Why only 15 dynamic tags?
* In /common/country_leader/
  - In '00_traits.txt': `ai_will_do` factor meaning?
  - `military_theorist` has `ai_will_do` with `factor = 500`. Too strong compared
  to other leaders? `mobile_warfare_expert` also.
* In /common/country_tags/
  - In '00_countries.txt': West Germany and East Germany have dual leader
  problem (Konrad Adenauer).

# R1 - 2016-06-15
* In /common/
  - 'ai_attitudes.txt' and 'ai_personalities.txt' file is completely blank. Why?
  - In 'graphicalculturetype.txt', commonwealth_2d is missing. Why? -->
  It is WAD. Commonwealth countries use `western_european_2d`.
  - 'static_modifiers.txt' has all global modifiers.
  - 'triggered_modifiers.txt' is blank. Intentional?
* In /common/ai_focuses/
  - ENG, FRA, GER, ITA, JAP, POL, SOV, USA has historical focus list.
  - Every focus decision seems to based on probability weight.
  - Maybe I can tweak a little bit in 'generic.txt' for better minor nation AI.
  - Every minor nation has same focus spec? Unacceptable. Minor nations should
  be more categorized. But DLC and expansion packs will take care of this.
  - __TODO:__ Exact meaning of values (ex: air_doctrine = 50.0) should be
  determined to edit these.
* In /common/ai_peace/
  - Peace conference strategy script.
  - `Civil war -> {Communist, Fascist, Democratic} -> Default` priority in this
  order.
* In /common/ai_strategy/
  - In 'default.txt': `default_unit_production`. This is very important for
  making AI to use more MT and HT battalions in division templates.
  - `default_paratroopers_production`. It is only enabled when
  `ai_wants_divisions > 94`. It is quite intuitive decision because a nation
  with less than 95 divisions will not need paratroopers anyway.
  - `unit_base` values seem to be additive. For example, base infantry unit_base
  is 90. If `default_paratroopers_production` item is enabled, then it will
  change `infantry` by -2 and change `paratroopers` by +2.
  - __TODO:__ `default_marines_production` needs more conditions, because
  landlocked countries such as Austria do not need marines at all. In this case,
  mountaineer should get priority.
  - Producing both motorized and mechanized seems contradictory. If a nation
  have enough tech/resource/factory output, then it is almost always better to
  produce mechanized infantry. Otherwise, sticking to motrized infantry is
  better for economic viewpoint. Producing both at the same time is non
  optimal, I think.
  - `slightly_naval_focused_nation`, `more_naval_focused_nation`,
  `less_naval_focused_nation`. Nation tags (JAP, GER, USA, ...) and date
  (`date < "1938.1.1"`) conditions are used.
