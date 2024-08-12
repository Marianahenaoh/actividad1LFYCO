class DFA:
    def __init__(self, num_states, alphabet, final_states, transitions):
        self.num_states = num_states
        self.alphabet = alphabet
        self.final_states = set(final_states)
        self.transitions = transitions  # Transiciones representadas como una lista de listas

    def is_final(self, state):
        return state in self.final_states

def minimize_dfa(dfa):
    num_states = dfa.num_states
    alphabet = dfa.alphabet
    table = [[False] * num_states for _ in range(num_states)]

    # Marcar pares de estados (p, q) donde uno es final y el otro no lo es
    for i in range(num_states):
        for j in range(i + 1, num_states):
            if (dfa.is_final(i) and not dfa.is_final(j)) or (not dfa.is_final(i) and dfa.is_final(j)):
                table[i][j] = True

    # Marcar pares de estados que pueden distinguirse por una secuencia de transiciones
    while True:
        updated = False
        for i in range(num_states):
            for j in range(i + 1, num_states):
                if not table[i][j]:
                    for symbol in alphabet:
                        p = dfa.transitions[i][alphabet.index(symbol)]
                        q = dfa.transitions[j][alphabet.index(symbol)]
                        if p > q:
                            p, q = q, p
                        if table[p][q]:
                            table[i][j] = True
                            updated = True
                            break
        if not updated:
            break

    # Identificar los estados equivalentes
    equivalent_pairs = []
    for i in range(num_states):
        for j in range(i + 1, num_states):
            if not table[i][j]:
                equivalent_pairs.append((i, j))

    return equivalent_pairs

def process_input():
    num_cases = int(input().strip())
    cases = []

    for _ in range(num_cases):
        num_states = int(input().strip())
        alphabet = input().strip().split()
        final_states = list(map(int, input().strip().split()))

        transitions = []
        for _ in range(num_states):
            transition = list(map(int, input().strip().split()))
            transitions.append(transition)

        cases.append(DFA(num_states, alphabet, final_states, transitions))

    return cases

def main():
    cases = process_input()
    print()
    for dfa in cases:
        equivalent_pairs = minimize_dfa(dfa)
        equivalent_pairs.sort()  # Ordenar lexicográficamente
        output = " ".join(f"{p} {q}" for p, q in equivalent_pairs)  # Aquí se ajusta la salida
        print(output)

if __name__ == "__main__":
    main()
