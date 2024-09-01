# Usage

Use the "Launch Root Error Reporting Actor" and "Launch Nested Error Reporting Actor" in place of the usual actor framework launchers.

Create children of the "Error Reporter" actor for actors in your regular project.

Create children of the "Error Manager" actor and override its "Error" method to alter how errors from actors in your project are handled, e.g. displaying a pop-up message and logging the error to a file. No functionality is provided in the default "Error Manager" actor.

# How it Works

The "Error Manager" actor is launched as a root actor. "Error Reporter" actors have the "Error Manager" actor's message enqueuer added to their private data on creation. The "Handle Error" method of the "Error Reporter" actor is overriden, and sends the error in a message to the "Error Manager". The stop core method of the "Error Reporter" actor is overridden to send a stop message to the "Error Manager" actor, ensuring shutdown of the separate "Error Manager" actor tree.
