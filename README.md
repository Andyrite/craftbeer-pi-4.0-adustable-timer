import time
from craftbeerpi import Plugin

class AdjustableActorsPlugin(Plugin):
    def __init__(self):
        super().__init__()
        self.actors = {}
        
    def add_actor(self, name, interval):
        """Add an actor with a specified time interval."""
        self.actors[name] = {'interval': interval, 'enabled': True}
        
    def remove_actor(self, name):
        """Remove an actor."""
        if name in self.actors:
            del self.actors[name]

    def set_interval(self, name, interval):
        """Set a new interval for an actor."""
        if name in self.actors:
            self.actors[name]['interval'] = interval

    def toggle_actor(self, name):
        """Enable or disable an actor."""
        if name in self.actors:
            self.actors[name]['enabled'] = not self.actors[name]['enabled']

    def run(self):
        """Main loop for the plugin."""
        while True:
            for name, actor in self.actors.items():
                if actor['enabled']:
                    # Execute the actor's function here
                    print(f"Running actor: {name}")
                    
                    # Sleep for the actor's interval
                    time.sleep(actor['interval'])
            time.sleep(1)  # Small delay to prevent tight loop

# Register the plugin
plugin = AdjustableActorsPlugin()
