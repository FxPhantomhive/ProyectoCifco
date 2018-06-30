<?php
	require('conexion.php');
	

	$consulta = "SELECT u.idUsuario, concat(u.Nombre, ' ', u.Apellidos), d.NombreDocumento, u.NumDocumento, u.Empresa, u.CorreoElectronico, u.Telefono, p.NombrePais, c.NombreCategoria, ta.NombreTipoAcceso, f.urlFoto FROM usuarios u, documentos d, fotousuarios fu, paises p, categorias c, tipoaccesos ta, fotos f where u.idUsuario = fu.idUsuario and u.idPais= p.idPais and u.idCategoria = c.idCategoria and u.idTipoAcceso = ta.idTipoAcceso and u.idDocumento = d.idDocumento and fu.idFoto = f.idFoto";
	
	$resultado = mysqli_query( $conexion, $consulta ) or die ( "Algo ha ido mal en la consulta a la base de datos");	

?>


<html>
	<head>
		<title>Usuarios</title>
	</head>
	<body>
		
		<center><h1>Usuarios</h1></center>
		
		<a href="nuevo.php">Nuevo usuario</a>
		<p></p>
		
		<table>
			<thead>
				<tr>
					<td><b>id usuario</b></td>
					<td><b>usuario</b></td>
					<td><b>Tipo de documento</b></td>
					<td><b>Numero de documento</b></td>
					<td><b>Empresa</b></td>
					<td><b>E-Mail</b></td>
					<td><b>Telefono</b></td>
					<td><b>Pais</b></td>
					<td><b>Categoria</b></td>
					<td><b>Tipo de acceso</b></td>
					<td></td>
					<td></td>
				</tr>
				<tbody>
					<?php while($row=mysqli_fetch_array( $resultado )){ ?>
						<tr>
							<td><?php echo $row['idUsuario'];?>
							</td>
							<td><?php echo $row['concat(u.Nombre, ' ', u.Apellidos)'];?>
							</td>
							<td><?php echo $row['d.NombreDocumento'];?>
							</td>
							<td><?php echo $row['u.NumDocumento'];?>
							</td>
							<td><?php echo $row['u.Empresa'];?>
							</td>
							<td><?php echo $row['u.CorreoElectronico'];?>
							</td>
							<td><?php echo $row['u.Telefono'];?>
							</td>
							<td><?php echo $row['p.NombrePais'];?>
							</td>
							<td><?php echo $row['c.NombreCategoria'];?>
							</td>
							<td><?php echo $row['ta.NombreTipoAcceso'];?>
							</td>
							<td>
								<a href="modificar.php?id=<?php echo $row['id'];?>">Modificar</a>
							</td>
							<td>
								<a href="eliminar.php?id=<?php echo $row['id'];?>">Eliminar</a>
							</td>
						</tr>
					<?php } ?>
				</tbody>
			</table>
		</body>
	</html>	
	
