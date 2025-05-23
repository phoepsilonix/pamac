gobject = dependency('gobject-2.0')
gio = dependency('gio-2.0')
libnotify = dependency('libnotify')
gio_unix = dependency('gio-unix-2.0')

libpamac = dependency('pamac', version : '>=11.7')

gtk3 = dependency('gtk+-3.0', version : '>=3.24')
gtk4 = dependency('gtk4', version : '>=4.10')
libadwaita = dependency('libadwaita-1', version : '>=1.4')


common_vala_args = ['--pkg=posix', '--vapidir=' + join_paths(meson.global_source_root(), 'vapi')]
common_c_args = ['-DGETTEXT_PACKAGE="pamac"']

executable('pamac-tray',
	sources: ['tray.vala', 'tray-gtk.vala'],
	dependencies: [gtk3, libnotify, libpamac],
	vala_args: common_vala_args,
	c_args: common_c_args,
	install: true)

libpamac_gtk = library('pamac-gtk',
	sources: ['transaction-gtk.vala', 'choose_provider_dialog.vala', 'choose_pkgs_dialog.vala',
			'transaction_sum_dialog.vala', 'summary_row.vala', 'progress_box.vala', 'version.vala',
			'local_config.vala', 'database-gtk.vala', transaction_resources],
	dependencies: [gtk4, libadwaita, libpamac],
	vala_args: common_vala_args,
	c_args: common_c_args,
	install: true,
	install_dir: [true])

libpamac_gtk_dep = declare_dependency(link_with: libpamac_gtk)

executable('pamac-manager',
	sources: ['version.vala', 'history_dialog.vala', 'updates_dialog.vala', 'preferences_dialog.vala',
			'package_row.vala', 'simple_row.vala', 'back_row.vala', 'manager_window.vala', 'manager.vala',
			'search-provider.vala', manager_resources],
	dependencies: [gtk4, libadwaita, gio_unix, libpamac, libpamac_gtk_dep],
	vala_args: common_vala_args,
	c_args: common_c_args,
	install: true)

if get_option('enable-fake-gnome-software')
	executable('gnome-software',
		sources: ['fake_gnome_software.vala'],
		dependencies: [gio],
		install: true)
endif

executable('pamac-installer',
	sources: ['progress_dialog.vala', 'installer.vala', installer_resources],
	dependencies: [gtk4, libadwaita, gio_unix, libpamac, libpamac_gtk_dep],
	vala_args: common_vala_args,
	c_args: common_c_args,
	install: true)
