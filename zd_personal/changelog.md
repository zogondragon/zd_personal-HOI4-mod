# R1 - 2016-06-15
* In /common/
  - 'ai_attitudes.txt' and 'ai_personalities.txt' file is completely blank. Why?
  - In 'graphicalculturetype.txt', commonwealth_2d is missing. Why?
  - 'static_modifiers.txt' has all global modifiers.
  - 'triggered_modifiers.txt' is blank. Intentional?
* In /common/ai_focuses/
  - ENG, FRA, GER, ITA, JAP, POL, SOV, USA has historical focus list.
  - Every focus decision seems to based on probability weight.
  - Maybe I can tweak a little bit in 'generic.txt' for better minor nation AI.
  - Every minor nation has same focus spec? Unacceptable. Minor nations should
  be more categorized. But DLC and expansion packs will take care of this.
  - __TODO:__ Exact meaning of values (ex: air_doctrine = 50.0) should be determined
  to edit these.
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
  - 
