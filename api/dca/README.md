# Data Container Arrays

Data Container Arrays (DCAs) are used to store table meta data. Each DCA
describes a particular table in terms of its configuration, its relations to
other tables and its fields. The Contao core engine determines by this meta data
how to list records, how to render back end forms and how to save data. The DCA
files of all active module are loaded one after the other (starting with
"backend" and "frontend" and then in alphabetical order), so that every module
can override the existing configuration. The `system/config/dcaconfig.php` file
is included at the end.
