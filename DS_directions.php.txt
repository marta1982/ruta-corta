<?php
	//cargamos el objeto usuario logueado
	global $user;

	if ($user->uid != 0) {

		// ID de usuario
		$user_data = user_load($user->uid);

		// datos de la localización del usuario
		$user_latitude = $user_data->field_location['und'][0]['latitude'];
		$user_longitude = $user_data->field_location['und'][0]['longitude'];
		$fromlocs = $user_data->field_location['und'][0]['name'];
		$fromlatlon = $user_latitude . "," . $user_longitude;

		// comprobamos que el usuario haya introducido su localización
		if ($user_latitude) {
			//datos de la localización del evento a partir del objeto $entity
			$tolocs = $entity->field_location['und'][0]['name'];
			$tolat = $entity->field_location['und'][0]['latitude'];
			$tolon = $entity->field_location['und'][0]['longitude'];
			$tolatlon = $tolat . "," . $tolon;

			//función que saca la ruta con el módulo https://www.drupal.org/project/getdirections
			return getdirections_locations_bylatlon($fromlocs, $fromlatlon, $tolocs, $tolatlon);
		}
		//si el usuario no tiene localización le invitamos a que lo haga
		else {
			print "No has configurado tu localización. Si quieres ver la ruta, entra en tu perfíl de usuario y añadela";
		}
	}

?>