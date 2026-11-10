import numpy as np

class TetrahedralNode:
    def __init__(self, node_id, coordinates):
        self.node_id = node_id
        self.coords = np.array(coordinates, dtype=float)
        self.neighbors = []
        self.state = 0.0  # Information/energy potential state

    def connect(self, other_node):
        if other_node not in self.neighbors:
            self.neighbors.append(other_node)
        if self not in other_node.neighbors:
            other_node.neighbors.append(self)

class TetrahedralMatrixSimulator:
    def __init__(self):
        self.nodes = {}
        self._initialize_base_tetrahedron()

    def _initialize_base_tetrahedron(self):
        # The 4 vertices of a regular tetrahedron in 3D space
        # Symmetrical and equidistant from each other
        v_coords = {
            0: ( 1.0,  1.0,  1.0),
            1: ( 1.0, -1.0, -1.0),
            2: (-1.0,  1.0, -1.0),
            3: (-1.0, -1.0,  1.0)
        }
        
        # Instantiate nodes
        for n_id, coords in v_coords.items():
            self.nodes[n_id] = TetrahedralNode(n_id, coords)

        # Connect every node to every other node (a complete graph 
        # is the fundamental property of a single tetrahedron)
        for i in range(4):
            for j in range(i + 1, 4):
                self.nodes[i].connect(self.nodes[j])

    def inject_pulse(self, node_id, magnitude=1.0):
        """Injects an information pulse into a specific node."""
        if node_id in self.nodes:
            self.nodes[node_id].state += magnitude

    def step(self, decay=0.1, propagation_factor=0.5):
        """
        Simulates one cycle of non-local spatial propagation across 
        the tetrahedral web, simulating wave interference.
        """
        new_states = {n_id: node.state * (1.0 - decay) for n_id, node in self.nodes.items()}
        
        for n_id, node in self.nodes.items():
            for neighbor in node.neighbors:
                # Energy distributes symmetrically across geometric connections
                new_states[n_id] += neighbor.state * propagation_factor * (1.0 / len(node.neighbors))

        # Update states
        for n_id, node in self.nodes.items():
            node.state = new_states[n_id]

    def get_state_snapshot(self):
        return {n_id: round(node.state, 4) for n_id, node in self.nodes.items()}

# --- Execution Example ---
if __name__ == "__main__":
    sim = TetrahedralMatrixSimulator()
    
    print("Initial State:", sim.get_state_snapshot())
    
    # Inject an information pulse into Node 0
    sim.inject_pulse(0, magnitude=10.0)
    print("After Injecting Pulse at Node 0:", sim.get_state_snapshot())
    
    # Run propagation cycles (wave distribution across the matrix)
    for step_num in range(1, 4):
        sim.step()
        print(f"Propagation Step {step_num}:", sim.get_state_snapshot())

import numpy as np

class TetrahedralNode:
    def __init__(self, node_id, coordinates):
        self.node_id = node_id
        self.coords = np.array(coordinates, dtype=float)
        self.neighbors = []
        self.state = 0.0  # Information/energy potential state

    def connect(self, other_node):
        if other_node not in self.neighbors:
            self.neighbors.append(other_node)
        if self not in other_node.neighbors:
            other_node.neighbors.append(self)

class TetrahedralMatrixSimulator:
    def __init__(self):
        self.nodes = {}
        self._initialize_base_tetrahedron()

    def _initialize_base_tetrahedron(self):
        # The 4 vertices of a regular tetrahedron in 3D space
        # Symmetrical and equidistant from each other
        v_coords = {
            0: ( 1.0,  1.0,  1.0),
            1: ( 1.0, -1.0, -1.0),
            2: (-1.0,  1.0, -1.0),
            3: (-1.0, -1.0,  1.0)
        }
        
        # Instantiate nodes
        for n_id, coords in v_coords.items():
            self.nodes[n_id] = TetrahedralNode(n_id, coords)

        # Connect every node to every other node (a complete graph 
        # is the fundamental property of a single tetrahedron)
        for i in range(4):
            for j in range(i + 1, 4):
                self.nodes[i].connect(self.nodes[j])

    def inject_pulse(self, node_id, magnitude=1.0):
        """Injects an information pulse into a specific node."""
        if node_id in self.nodes:
            self.nodes[node_id].state += magnitude

    def step(self, decay=0.1, propagation_factor=0.5):
        """
        Simulates one cycle of non-local spatial propagation across 
        the tetrahedral web, simulating wave interference.
        """
        new_states = {n_id: node.state * (1.0 - decay) for n_id, node in self.nodes.items()}
        
        for n_id, node in self.nodes.items():
            for neighbor in node.neighbors:
                # Energy distributes symmetrically across geometric connections
                new_states[n_id] += neighbor.state * propagation_factor * (1.0 / len(node.neighbors))

        # Update states
        for n_id, node in self.nodes.items():
            node.state = new_states[n_id]

    def get_state_snapshot(self):
        return {n_id: round(node.state, 4) for n_id, node in self.nodes.items()}

# --- Execution Example ---
if __name__ == "__main__":
    sim = TetrahedralMatrixSimulator()
    
    print("Initial State:", sim.get_state_snapshot())
    
    # Inject an information pulse into Node 0
    sim.inject_pulse(0, magnitude=10.0)
    print("After Injecting Pulse at Node 0:", sim.get_state_snapshot())
    
    # Run propagation cycles (wave distribution across the matrix)
    for step_num in range(1, 4):
        sim.step()
        print(f"Propagation Step {step_num}:", sim.get_state_snapshot())






