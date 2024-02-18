

import java.util.Scanner;

class Graph {
    private int[][] weights;

    public Graph(int layers, int[] nodes) {
        int totalNodes = 0;
        for (int nodeCount : nodes) {
            totalNodes += nodeCount;
        }
        weights = new int[totalNodes][totalNodes];
    }

    public void setEdgeWeight(int fromNode, int toNode, int weight) {
        weights[fromNode][toNode] = weight;
    }

    public int getEdgeWeight(int fromNode, int toNode) {
        return weights[fromNode][toNode];
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of layers: ");
        int layers = scanner.nextInt();

        int[] nodesInLayer = new int[layers];
        for (int i = 0; i < layers; i++) {
            System.out.print("Enter the number of nodes in layer " + (i + 1) + ": ");
            nodesInLayer[i] = scanner.nextInt();
        }

        Graph graph = new Graph(layers, nodesInLayer);

        for (int i = 0; i < nodesInLayer.length - 1; i++) {
            for (int j = 0; j < nodesInLayer[i]; j++) {
                for (int k = 0; k < nodesInLayer[i + 1]; k++) {
                    System.out.print("Enter weight from node " + j + " in layer " + (i + 1) + " to node " +
                            k + " in layer " + (i + 2) + ": ");
                    int weight = scanner.nextInt();
                    graph.setEdgeWeight(getNodeIndex(i, j, nodesInLayer), getNodeIndex(i + 1, k, nodesInLayer), weight);
                }
            }
        }

        // Querying edge weights
        System.out.print("Enter the source node: ");
        int sourceNode = scanner.nextInt();
        System.out.print("Enter the destination node: ");
        int destinationNode = scanner.nextInt();

        int weight = graph.getEdgeWeight(sourceNode, destinationNode);
        System.out.println("Weight from node " + sourceNode + " to node " + destinationNode + " is: " + weight);

        scanner.close();
    }

    private static int getNodeIndex(int layer, int node, int[] nodesInLayer) {
        int index = 0;
        for (int i = 0; i < layer; i++) {
            index += nodesInLayer[i];
        }
        index += node;
        return index;
    }
}
