# Contao callbacks

Callbacks are entry-points for custom code in the DCA. Using callbacks you
can modify static Data Container Array during runtime.

Callbacks are very similar to [Hooks][1], but always bound to a specific DCA table
and can have a different registration scheme (e.g. they only support one
callback function).


## Config callbacks

- onload\_callback
- onsumbit\_callback
- oncreate\_callback
- oncopy\_callback
- oncut\_callback
- ondelete\_callback


## List callbacks

- label\_callback
- group\_callback
- child\_record\_callback
- button\_callback
- paste\_button\_callback


## Field callbacks

- options\_callback
- load_callback
- save_callback
- input\_field\_callback



[1]: hooks.md