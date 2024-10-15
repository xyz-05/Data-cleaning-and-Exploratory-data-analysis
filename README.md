# Data-cleaning-and-Exploratory-data-analysis
# Data Cleaning and EDA on Titanic Dataset

def load_data():
    data = []
    with open('titanic.csv', 'r') as file:
        for line in file:
            data.append(line.strip().split(','))
    return data


def clean_data(data):
    cleaned_data = []
    for row in data[1:]:
        if '' not in row:  # Remove rows with missing values
            cleaned_data.append(row)
    return cleaned_data


def get_summary_statistics(data):
    summary = {}
    for i in range(len(data[0])):
        column = [row[i] for row in data]
        summary[data[0][i]] = {
            'count': len(column),
            'unique': len(set(column)),
            'mean': sum(map(float, column[1:])) / (len(column) - 1) if i != 0 else None
        }
    return summary


def explore_relationships(data):
    relationships = {}
    for i in range(1, len(data[0])):
        for j in range(i + 1, len(data[0])):
            col1 = [row[i] for row in data]
            col2 = [row[j] for row in data]
            relationships[(data[0][i], data[0][j])] = {
                'correlation': sum(map(float, col1[1:])) / (len(col1) - 1) * sum(map(float, col2[1:])) / (len(col2) - 1)
            }
    return relationships

def main():
    data = load_data()
    cleaned_data = clean_data(data)
    summary_statistics = get_summary_statistics(cleaned_data)
    relationships = explore_relationships(cleaned_data)

    print("Summary Statistics:", summary_statistics)
    print("Relationships:", relationships)

main()
