import numpy as np

# Define the fitness function to be optimized
def fitness(x):
    return np.sum(x**2)

# Define the Wolf Pack Optimization algorithm
def wolf_pack_optimization(fitness, dim, lb, ub, n, max_iter):
    # Initialize the position of the alpha, beta, and delta wolves
    alpha_pos = np.zeros(dim)
    beta_pos = np.zeros(dim)
    delta_pos = np.zeros(dim)
    alpha_score = float('inf')
    beta_score = float('inf')
    delta_score = float('inf')

    # Initialize the position of the other wolves
    positions = np.random.uniform(lb, ub, (n, dim))

    # Main loop
    for i in range(max_iter):
        # Update the position of the alpha wolf
        for j in range(n):
            score = fitness(positions[j])
            if score < alpha_score:
                alpha_pos = positions[j].copy()
                alpha_score = score

        # Update the position of the beta wolf
        for j in range(n):
            if np.array_equal(positions[j], alpha_pos):
                continue
            score = fitness(positions[j])
            if score < beta_score:
                beta_pos = positions[j].copy()
                beta_score = score

        # Update the position of the delta wolf
        for j in range(n):
            if np.array_equal(positions[j], alpha_pos) or np.array_equal(positions[j], beta_pos):
                continue
            score = fitness(positions[j])
            if score < delta_score:
                delta_pos = positions[j].copy()
                delta_score = score

        # Update the position of the other wolves
        for j in range(n):
            r1 = np.random.rand(dim)
            r2 = np.random.rand(dim)
            A = 2 * r1 - 1
            C = 2 * r2
            D_alpha = np.abs(C * alpha_pos - positions[j])
            X1 = alpha_pos - A * D_alpha

            r1 = np.random.rand(dim)
            r2 = np.random.rand(dim)
            A = 2 * r1 - 1
            C = 2 * r2
            D_beta = np.abs(C * beta_pos - positions[j])
            X2 = beta_pos - A * D_beta

            r1 = np.random.rand(dim)
            r2 = np.random.rand(dim)
            A = 2 * r1 - 1
            C = 2 * r2
            D_delta = np.abs(C * delta_pos - positions[j])
            X3 = delta_pos - A * D_delta

            positions[j] = (X1 + X2 + X3) / 3

    return alpha_pos, alpha_score

# Example usage
dim = 10
lb = -10
ub = 10
n = 30
max_iter = 1000

solution, score = wolf_pack_optimization(fitness, dim, lb, ub, n, max_iter)

print("Solution: ", solution)
print("Fitness score: ", score)
