
appdatadir = $(datadir)/appdata
appdata_in_files =

appdata_DATA = $(appdata_in_files:.xml.in=.xml)
@INTLTOOL_XML_RULE@

if USE_DBUS
exec_command = 'genericdiscordalternative --existing %U'
else
exec_command = 'genericdiscordalternative %U'
endif

genericdiscordalternative.desktop.in: genericdiscordalternative.desktop.in.in
	$(AM_V_GEN)sed -e s!\@exec_command\@!$(exec_command)! < $< > $@

data_desktopdir = $(datadir)/applications
data_desktop_in_files =

if DO_GTK
data_desktop_in_files += genericdiscordalternative.desktop.in
endif

if WITH_TM
data_desktop_in_files += htm.desktop.in
mime_DATA = htm-mime.xml
mimedir = $(datadir)/mime/packages
endif

data_desktop_DATA = $(data_desktop_in_files:.desktop.in=.desktop)
@INTLTOOL_DESKTOP_RULE@

UPDATE_MIME_DATABASE = update-mime-database "$(datadir)/mime" || :
UPDATE_DESKTOP_DATABASE = update-desktop-database -q "$(datadir)/applications" || :

install-data-hook:
	$(UPDATE_MIME_DATABASE);
	$(UPDATE_DESKTOP_DATABASE);

uninstall-hook:
	$(UPDATE_MIME_DATABASE);
	$(UPDATE_DESKTOP_DATABASE);

EXTRA_DIST = genericdiscordalternative.desktop.in.in htm.desktop.in htm-mime.xml

CLEANFILES = $(appdata_DATA) $(data_desktop_DATA) genericdiscordalternative.desktop.in
