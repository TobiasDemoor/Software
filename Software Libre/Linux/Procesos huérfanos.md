---
aliases: ["procesos huérfanos", "proceso huérfano", "re-crianza"]
---
En un sistema operativo tipo [[Unix]], **cualquier proceso huérfano será adoptado inmediatamente por el proceso especial del sistema init**: el kernel establece el padre en init. Esta operación se llama re-crianza y ocurre automáticamente. Aunque técnicamente el proceso tiene el proceso "init" como padre, todavía se le llama proceso huérfano ya que el proceso que lo creó originalmente ya no existe.