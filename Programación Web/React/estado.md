El estado contiene datos específicos de este componente que pueden cambiar con el tiempo. El estado está definido por el usuario, y debe ser un simple objeto JavaScript.

Si no se utiliza algún valor para renderizar o simplemente flujos de datos (por ejemplo, un ID de temporizador), no tiene que ponerlo en el estado. Dichos valores se pueden definir como campos en la instancia del componente.

Consulta [Estado y Ciclo de Vida](https://es.reactjs.org/docs/state-and-lifecycle.html) para mas información sobre el estado.

Nunca mutes `this.state` directamente, ya que llamar `setState()` después podría reemplazar la mutación que habías hecho anteriormente. Intenta tratar `this.state` como si fuera inmutable.