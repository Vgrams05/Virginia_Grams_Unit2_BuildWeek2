# Virginia_Grams_Unit2_BuildWeek2

![Blog Post](https://vgrams05.github.io/)

![Peru/Puerto Rico Download page](https://dengueforecasting.noaa.gov/)

![Project File]({
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "Virginia_Grams_Unit2_BuildWeek2",
      "provenance": [],
      "collapsed_sections": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "p89V33C6z19_"
      },
      "source": [
        "#Dataset links\n",
        "\n",
        "This is the link to me datasets metadata.\n",
        "\n",
        "* https://dengueforecasting.noaa.gov/Training/dengue-metadata-san_juan_training.html\n",
        "\n",
        "* https://dengueforecasting.noaa.gov/Training/dengue-metadata-iquitos_training.html\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "sF6VXvE6itII"
      },
      "source": [
        "#Blog Link\n",
        "\n",
        "Here is my blog for my Dengue project\n",
        "\n",
        "* [Portfolio site](https://vgrams05.github.io/)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "MEW6tvizi56a"
      },
      "source": [
        "#Cleaning the datasets\n",
        "\n",
        "Starting here I have cleaned, wrangled and combined my datasets. I wanted to combine peru and puerto rico datasets to give us a better undering of the dengue strains. Then I wrangled the data with dropping columns and adding an index. "
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "3r-lZVfisCcR"
      },
      "source": [
        "%%capture\n",
        "import sys\n",
        "\n",
        "!pip install category_encoders==2.*"
      ],
      "execution_count": 1,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "50Jy9SpDvd92"
      },
      "source": [
        "#Printing the Dataframes\n",
        "import numpy as np\n",
        "import pandas as pd\n",
        "import codecs\n",
        "\n",
        "peru = pd.read_csv('/content/Iquitos_Training_Data.csv')\n",
        "rico = pd.read_csv('/content/San_Juan_Training_Data.csv')"
      ],
      "execution_count": 2,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Ml9kFwh0qHdp",
        "outputId": "d1a62d6b-7d22-40bf-f66c-1a9a0343f9c2",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 215
        }
      },
      "source": [
        "#Combing the two datasets\n",
        "frame = [rico, peru]\n",
        "\n",
        "result = pd.concat(frame)\n",
        "\n",
        "result.head()"
      ],
      "execution_count": 3,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>season</th>\n",
              "      <th>season_week</th>\n",
              "      <th>week_start_date</th>\n",
              "      <th>denv1_cases</th>\n",
              "      <th>denv2_cases</th>\n",
              "      <th>denv3_cases</th>\n",
              "      <th>denv4_cases</th>\n",
              "      <th>other_positive_cases</th>\n",
              "      <th>additional_cases</th>\n",
              "      <th>total_cases</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1990/1991</td>\n",
              "      <td>1</td>\n",
              "      <td>1990-04-30</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>4</td>\n",
              "      <td>0.0</td>\n",
              "      <td>4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1990/1991</td>\n",
              "      <td>2</td>\n",
              "      <td>1990-05-07</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>5</td>\n",
              "      <td>0.0</td>\n",
              "      <td>5</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1990/1991</td>\n",
              "      <td>3</td>\n",
              "      <td>1990-05-14</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>4</td>\n",
              "      <td>0.0</td>\n",
              "      <td>4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1990/1991</td>\n",
              "      <td>4</td>\n",
              "      <td>1990-05-21</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>3</td>\n",
              "      <td>0.0</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1990/1991</td>\n",
              "      <td>5</td>\n",
              "      <td>1990-05-28</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>6</td>\n",
              "      <td>0.0</td>\n",
              "      <td>6</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "      season  season_week  ... additional_cases  total_cases\n",
              "0  1990/1991            1  ...              0.0            4\n",
              "1  1990/1991            2  ...              0.0            5\n",
              "2  1990/1991            3  ...              0.0            4\n",
              "3  1990/1991            4  ...              0.0            3\n",
              "4  1990/1991            5  ...              0.0            6\n",
              "\n",
              "[5 rows x 10 columns]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 3
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "mTsRbPQonVxg",
        "outputId": "a358ddb9-8eda-4d3e-8432-3aa027c52749",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Checking to see what would be best to drop from the dataframe\n",
        "result.info()"
      ],
      "execution_count": 4,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "Int64Index: 1456 entries, 0 to 467\n",
            "Data columns (total 10 columns):\n",
            " #   Column                Non-Null Count  Dtype  \n",
            "---  ------                --------------  -----  \n",
            " 0   season                1456 non-null   object \n",
            " 1   season_week           1456 non-null   int64  \n",
            " 2   week_start_date       1456 non-null   object \n",
            " 3   denv1_cases           1456 non-null   int64  \n",
            " 4   denv2_cases           1456 non-null   int64  \n",
            " 5   denv3_cases           1456 non-null   int64  \n",
            " 6   denv4_cases           1456 non-null   int64  \n",
            " 7   other_positive_cases  1456 non-null   int64  \n",
            " 8   additional_cases      988 non-null    float64\n",
            " 9   total_cases           1456 non-null   int64  \n",
            "dtypes: float64(1), int64(7), object(2)\n",
            "memory usage: 125.1+ KB\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "z3gOhthmncFR"
      },
      "source": [
        "#wrangle the data by dropping columns and making an index.\n",
        "def wrangle(X):\n",
        " X = X.copy()\n",
        " X.drop(columns =['additional_cases', 'other_positive_cases', 'season'], inplace=True)\n",
        " X.set_index('week_start_date', inplace=True)\n",
        "\n",
        " return X\n",
        "\n",
        "df = wrangle(result)"
      ],
      "execution_count": 5,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "OsxTlC3HnhKz",
        "outputId": "ab0f1a49-2a39-4b5d-d83e-27b3dc39acda",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 245
        }
      },
      "source": [
        "df.tail()"
      ],
      "execution_count": 6,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>season_week</th>\n",
              "      <th>denv1_cases</th>\n",
              "      <th>denv2_cases</th>\n",
              "      <th>denv3_cases</th>\n",
              "      <th>denv4_cases</th>\n",
              "      <th>total_cases</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>week_start_date</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>2009-05-28</th>\n",
              "      <td>48</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>1</td>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-04</th>\n",
              "      <td>49</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-11</th>\n",
              "      <td>50</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>2</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-18</th>\n",
              "      <td>51</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>3</td>\n",
              "      <td>5</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-25</th>\n",
              "      <td>52</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>1</td>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "                 season_week  denv1_cases  ...  denv4_cases  total_cases\n",
              "week_start_date                            ...                          \n",
              "2009-05-28                48            0  ...            1            2\n",
              "2009-06-04                49            0  ...            1            3\n",
              "2009-06-11                50            0  ...            2            3\n",
              "2009-06-18                51            0  ...            3            5\n",
              "2009-06-25                52            0  ...            1            2\n",
              "\n",
              "[5 rows x 6 columns]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 6
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "DqI4AM_5paZ9",
        "outputId": "6b3a8ee7-f8e3-4f35-dbfa-553be8a06c5e",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 304
        }
      },
      "source": [
        "df.describe()"
      ],
      "execution_count": 7,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>season_week</th>\n",
              "      <th>denv1_cases</th>\n",
              "      <th>denv2_cases</th>\n",
              "      <th>denv3_cases</th>\n",
              "      <th>denv4_cases</th>\n",
              "      <th>total_cases</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>1456.000000</td>\n",
              "      <td>1456.000000</td>\n",
              "      <td>1456.000000</td>\n",
              "      <td>1456.000000</td>\n",
              "      <td>1456.000000</td>\n",
              "      <td>1456.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>26.500000</td>\n",
              "      <td>0.987637</td>\n",
              "      <td>1.330357</td>\n",
              "      <td>2.818681</td>\n",
              "      <td>0.885989</td>\n",
              "      <td>25.182692</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>15.013488</td>\n",
              "      <td>2.750042</td>\n",
              "      <td>2.890451</td>\n",
              "      <td>6.295263</td>\n",
              "      <td>3.081156</td>\n",
              "      <td>43.524906</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>1.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>13.750000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>5.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>26.500000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>13.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>39.250000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>3.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>29.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>52.000000</td>\n",
              "      <td>27.000000</td>\n",
              "      <td>30.000000</td>\n",
              "      <td>74.000000</td>\n",
              "      <td>43.000000</td>\n",
              "      <td>461.000000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "       season_week  denv1_cases  ...  denv4_cases  total_cases\n",
              "count  1456.000000  1456.000000  ...  1456.000000  1456.000000\n",
              "mean     26.500000     0.987637  ...     0.885989    25.182692\n",
              "std      15.013488     2.750042  ...     3.081156    43.524906\n",
              "min       1.000000     0.000000  ...     0.000000     0.000000\n",
              "25%      13.750000     0.000000  ...     0.000000     5.000000\n",
              "50%      26.500000     0.000000  ...     0.000000    13.000000\n",
              "75%      39.250000     1.000000  ...     1.000000    29.000000\n",
              "max      52.000000    27.000000  ...    43.000000   461.000000\n",
              "\n",
              "[8 rows x 6 columns]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 7
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "JmYM_iZSp-P-",
        "outputId": "c233ecef-0615-42aa-bc0a-9fdb55a0a4d6",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Checking value_counts for 'season_week' to see if we will need it \n",
        "#'season_week' does match up to the 'week_start_date' index\n",
        "df['season_week'].value_counts()"
      ],
      "execution_count": 8,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "52    28\n",
              "51    28\n",
              "24    28\n",
              "23    28\n",
              "22    28\n",
              "21    28\n",
              "20    28\n",
              "19    28\n",
              "18    28\n",
              "17    28\n",
              "16    28\n",
              "15    28\n",
              "14    28\n",
              "13    28\n",
              "12    28\n",
              "11    28\n",
              "10    28\n",
              "9     28\n",
              "8     28\n",
              "7     28\n",
              "6     28\n",
              "5     28\n",
              "4     28\n",
              "3     28\n",
              "2     28\n",
              "25    28\n",
              "26    28\n",
              "27    28\n",
              "40    28\n",
              "50    28\n",
              "49    28\n",
              "48    28\n",
              "47    28\n",
              "46    28\n",
              "45    28\n",
              "44    28\n",
              "43    28\n",
              "42    28\n",
              "41    28\n",
              "39    28\n",
              "28    28\n",
              "38    28\n",
              "37    28\n",
              "36    28\n",
              "35    28\n",
              "34    28\n",
              "33    28\n",
              "32    28\n",
              "31    28\n",
              "30    28\n",
              "29    28\n",
              "1     28\n",
              "Name: season_week, dtype: int64"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 8
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "yYtkJmYCjLzs"
      },
      "source": [
        "#Split the data\n",
        "\n",
        "I have chosen 'total_cases' as my target. I will be training the data from all the data from 2009. Validation will be from 1990 to 1999. The test will be from 2000 to 2009."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "quX92_LonjL_"
      },
      "source": [
        "# Using total_cases as my target\n",
        "\n",
        "target = 'total_cases'\n",
        "y = df[target]\n",
        "X = df.drop(columns=target)"
      ],
      "execution_count": 9,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "HLtxGZJFnmFn"
      },
      "source": [
        "# Training will be from begining of 1990 to end of 2009\n",
        "X_train, y_train = X[:'2009-06-25'], y[:'2009-06-25']\n",
        "#Validation will be from start of cases in 1990 to end of 1999\n",
        "X_val, y_val = X['1990-04-30':'1999-12-24'], y['1990-04-30':'1999-12-24']\n",
        "#Testing will be from start of 2000 to the end of 2009 which is the last year of the dataset\n",
        "X_test, y_test = X['2000-01-01':'2009-06-25'], y['2000-01-01':'2009-06-25']"
      ],
      "execution_count": 10,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "wSBRj7Yujtqs"
      },
      "source": [
        "#Baseline"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "OuhKLLv2nqpH",
        "outputId": "11eb05a9-4c4c-495c-d5d8-71237b4562b0",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Building the baseline\n",
        "\n",
        "print('Baseline Accuracy:', y_train.value_counts(normalize=True).max())"
      ],
      "execution_count": 11,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Baseline Accuracy: 0.06524725274725275\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "aQ1pJSa1gOGd",
        "outputId": "aa456bcb-6862-4eb0-927e-0ec33ed61172",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Baseline MAE\n",
        "\n",
        "from sklearn.metrics import mean_absolute_error\n",
        "\n",
        "Y_pred = [y_train.mean()] * len(y_train)\n",
        "\n",
        "print('Baseline MAE:', mean_absolute_error(y_train, Y_pred))"
      ],
      "execution_count": 12,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Baseline MAE: 22.990252535925613\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "PVCpzqvyjxGl"
      },
      "source": [
        "#Building the model\n",
        "\n",
        "I have chosen XGB Classifier for my first model and LogisticRegression for my second."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "z_-_btI4rmKH",
        "outputId": "24151423-f0e4-4927-9181-1befb9ac959d",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "from category_encoders import OrdinalEncoder, OneHotEncoder\n",
        "from sklearn.impute import SimpleImputer\n",
        "from sklearn.pipeline import make_pipeline\n",
        "from xgboost import XGBClassifier\n",
        "from sklearn.linear_model import LogisticRegression\n",
        "from sklearn.preprocessing import StandardScaler"
      ],
      "execution_count": 13,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "/usr/local/lib/python3.6/dist-packages/statsmodels/tools/_testing.py:19: FutureWarning: pandas.util.testing is deprecated. Use the functions in the public API at pandas.testing instead.\n",
            "  import pandas.util.testing as tm\n"
          ],
          "name": "stderr"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "r7pj4baEsU3c"
      },
      "source": [
        "#Building the model using XGBClassifier\n",
        "eval_set = [(X_val, y_val)]\n",
        "\n",
        "model = make_pipeline(\n",
        "    OrdinalEncoder(),\n",
        "    SimpleImputer(),\n",
        "    XGBClassifier(n_estimators=400,\n",
        "                  random_state=42, \n",
        "                  eval_set=eval_set,\n",
        "                  eval_metric='merror',\n",
        "                  early_stopping_rounds=10,\n",
        "                  verbose=True,\n",
        "                  n_jobs=-1)\n",
        ")\n",
        "\n",
        "\n",
        "model.fit(X_train, y_train);"
      ],
      "execution_count": 14,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "bbnflynZcTAf",
        "outputId": "85a3c854-4eb4-4652-c717-ac69c672b166",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Building model two with LogisticRegression\n",
        "model_1 = make_pipeline(\n",
        "    OneHotEncoder(use_cat_names=True),\n",
        "    StandardScaler(),\n",
        "    SimpleImputer(),\n",
        "    LogisticRegression()\n",
        ")\n",
        "\n",
        "model_1.fit(X_train, y_train);"
      ],
      "execution_count": 15,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "/usr/local/lib/python3.6/dist-packages/category_encoders/utils.py:21: FutureWarning: is_categorical is deprecated and will be removed in a future version.  Use is_categorical_dtype instead\n",
            "  elif pd.api.types.is_categorical(cols):\n",
            "/usr/local/lib/python3.6/dist-packages/sklearn/linear_model/_logistic.py:940: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
            "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
            "\n",
            "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
            "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
            "Please also refer to the documentation for alternative solver options:\n",
            "    https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression\n",
            "  extra_warning_msg=_LOGISTIC_SOLVER_CONVERGENCE_MSG)\n"
          ],
          "name": "stderr"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "E1IOthGUtqEb",
        "outputId": "86e69e7b-732a-4e9e-d346-29b27c48a750",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Checking Metrics for model\n",
        "\n",
        "print('Training Accuracy:', model.score(X_train, y_train))\n",
        "print('Validation Accuracy:', model.score(X_val, y_val))"
      ],
      "execution_count": 16,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Training Accuracy: 0.6881868131868132\n",
            "Validation Accuracy: 0.7037773359840954\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "VRCO3MAldfow",
        "outputId": "78222546-e1a9-404c-bab3-78f0dcd642d1",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "# Checking Metrics for model_1\n",
        "print('Training Accuracy:', model_1.score(X_train, y_train))\n",
        "print('Validation Accuracy:', model_1.score(X_val, y_val))"
      ],
      "execution_count": 17,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Training Accuracy: 0.14972527472527472\n",
            "Validation Accuracy: 0.027833001988071572\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Ya1Xj1lBh7mt"
      },
      "source": [
        "#Score\n",
        "\n",
        "Between model and model_1, model has the better score so I will go with this one."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Zys8XewAuM9e",
        "outputId": "a527965b-ceca-418e-f47d-6f30573bfcba",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 296
        }
      },
      "source": [
        "#Communicating Results \n",
        "\n",
        "import matplotlib.pyplot as plt\n",
        "\n",
        "importances = model.named_steps['xgbclassifier'].feature_importances_\n",
        "\n",
        "feat_imp = pd.Series(importances, index=X_train.columns).sort_values()\n",
        "feat_imp.tail(10).plot(kind='barh')\n",
        "plt.xlabel('Gini importance')\n",
        "plt.ylabel('Feature')"
      ],
      "execution_count": 18,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Text(0, 0.5, 'Feature')"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 18
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "iVBORw0KGgoAAAANSUhEUgAAAbQAAAEGCAYAAAANNmA4AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAc3UlEQVR4nO3de5QeVZ3u8e9DgAACUSSyYlDCJQICJpIAioACCoyREY/hckTkooMwjLeRcXCBLsYryOhw8YBmHA3j5SSCCNEMAQQhISDkTghy0QRHg3MQEBQDAZLn/FG79aXtJG+S7n47O89nrXdRvatq1+8tmvWwd1VXyTYREREbuk06XUBERERvSKBFREQVEmgREVGFBFpERFQhgRYREVXYtNMFbKy23357jxgxotNlRERsUObMmfOY7aE9rUugdciIESOYPXt2p8uIiNigSPrVqtZlyjEiIqqQQIuIiCok0CIiogoJtIiIqEICLSIiqpBAi4iIKiTQIiKiCgm0iIioQgItIiKqkCeFdMjCpU8x4pypnS4jIqJfPXzBuD7rOyO0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCAi0iIqqQQIuIiCok0CIiogr9HmiSzpd0di/29zZJcyQtLP88rLf6joiIDUcNTwp5DDja9iOS9gZuAIZ3uKaIiOhn/TJCk3SupAcl3Q7sXtp2lTStjKpmSNqjtE+UdKmkOyQtljS+tE+SNK6lz4mSxtueZ/uR0rwI2FLS4NXUcpSkuZIWSLq5tO0v6U5J88pxu2rcS9LdkuZLukfSyNL+3pb2r0saVD4TJd1bRosf6+HYp0uaLWn2imVP9cq5jYiIRp+P0CSNAU4ARpfjzQXmABOAM2w/JOkA4HKga7pwGHAQsAcwBbgamAwcB0yVtDlwOHBmt8O9G5hre/kqahkK/DtwiO0lkrYrq+4HDrb9gqS3Al8ofZ0BXGL7u+WYgyTtCRwPvMn285IuB06kCdPhtvcux3pp9+PbnlC+N4OHjXR7ZzAiItrRH1OOBwM/tL0MQNIUYAvgQOAqSV3btY6qrrW9ErhP0g6l7XrgkjL6OgqYbvuZrh0k7QVcCByxmlreUPZbAmD7idI+BLiyjMAMbFba7wTOlbQjcE0J38OBMcCsUvuWwKPAj4BdJF0GTAVubPcERUTE+uvUNbRNgCdtj17F+tYRlgBsPyvpVuBImhHSpD9v0ATOD4H32f7lOtTzWeCntt8laQRwaznm9yTdBYwD/kvSB0s9V9r+ZPdOJI0q9Z1BM5o8bR1qiYiIddAf19CmA8dI2lLSNsDRwDJgiaRjAdQY1UZfk4FTaUZ908q+L6UZEZ1je+Ya9v8ZcIikncu+XVOOQ4ClZfmUro0l7QIstn0pcB3wOuBmYLykV3T1IWknSdsDm9j+AXAesG8b3yciInpJnwea7bk0QbSAZtpwVll1IvB+SQtorj+9s43ubgTeDPzE9nOl7R+A3YBPl5s05neFTQ+1/A44HbimHHdyWfUl4IuS5vHiUetxwL2S5gN7A/9p+z6awLpR0j3ATTTX/IYDt5ZtvwP81QguIiL6juzcm9AJg4eN9LCTL+50GRER/Wp9X/ApaY7tsT2ty5NCIiKiCjX8YXWPys0c3f8e7STbCztRT0RE9K1qA832AZ2uISIi+k+mHCMiogrVjtAGun2GD2H2el4cjYiIv8gILSIiqpBAi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCAi0iIqqQQIuIiCok0CIiogoJtIiIqEICLSIiqpBAi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCAi0iIqqwaacL2FgtXPoUI86Z2ukyIiJ6zcMXjOvo8TNCi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCvweapPMlnd2L/e0vaX75LJD0rt7qOyIiNhw1/GH1vcBY2y9IGgYskPQj2y90urCIiOg//TJCk3SupAcl3Q7sXtp2lTRN0hxJMyTtUdonSrpU0h2SFksaX9onSRrX0udESeNtL2sJry0Ar6GW90m6p4zmvl3ajpZ0l6R5kn4iaYfS/uaW0d88SduU9n+SNKv08y+l7SWSppZ+75V0fK+exIiIWK0+H6FJGgOcAIwux5sLzAEmAGfYfkjSAcDlwGFlt2HAQcAewBTgamAycBwwVdLmwOHAmeUYBwDfBHYCTlrV6EzSXsB5wIG2H5O0XVl1O/AG25b0AeATwMeBs4GzbM+UtDXwrKQjgJHA/oCAKZIOAYYCj9geV441pIfjnw6cDjBo26FrdyIjImK1+mPK8WDgh7aXAUiaQjOSOhC4SlLXdoNb9rnW9krgvq7REnA9cImkwcBRwHTbzwDYvgvYS9KewJWSrrf9bA+1HAZcZfuxst8TpX1HYHKZstwcWFLaZwJfkfRd4BrbvymBdgQwr2yzNU3AzQC+LOlC4Me2Z3Q/uO0JNEHO4GEjVzuSjIiItdOpuxw3AZ60Pbrls2fL+uUtywIoAXUrcCRwPM2I7UVs/xx4Gth7Leu5DPiq7X2AD9IELrYvAD4AbAnMLNOiAr7YUvdutv/D9oPAvsBC4HOSPr2WNURExHroj0CbDhwjactyDepoYBmwRNKxAGqMaqOvycCpNKO+aWXfnSVtWpZ3opmmfHgV+98CHCvp5WX7rinHIcDSsnxy18aSdrW90PaFwKzS9w3AaWUKEknDJb1C0iuBZba/A1xEE24REdFP+nzK0fZcSZOBBcCjNMEAcCJwhaTzgM2ASWWb1bkR+DZwne3nSttBwDmSngdWAn/fNaXYQy2LJH0euE3SCpppw1OA82mmP39PE3o7l10+KunQ0u8i4Hrby8vU5p1luvRp4L3AbsBFklYCz1Ou70VERP+QnUs5nTB42EgPO/niTpcREdFr+uN9aJLm2B7b07o8KSQiIqpQwx9W/5VyjezmHlYdbvvx/q4nIiL6XpWBVkJrdKfriIiI/pMpx4iIqEKVI7QNwT7DhzC7Hy6gRkRsLDJCi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCAi0iIqqQQIuIiCok0CIiogoJtIiIqEICLSIiqpBAi4iIKiTQIiKiCgm0iIioQgItIiKq0HagSdpS0u59WUxERMS6aivQJB0NzAemlZ9HS5rSl4VFRESsjXZHaOcD+wNPAtieD+zcRzVFRESstXYD7XnbT3Vrc28XExERsa42bXO7RZLeAwySNBL4MHBH35UVERGxdmSveaAlaSvgXOCI0nQD8Dnbz/ZhbVUbPGykh518cafLiIj4s4cvGNfpEtZI0hzbY3tat8YRmqRBwFTbh9KEWkRExICzxmtotlcAKyUN6Yd6IiIi1km719CeBhZKugn4U1ej7Q/3SVURERFrqd1Au6Z8IiIiBqS2As32lX1dSERExPpoK9AkLaGHvzuzvUuvVxQREbEO2p1ybL1FcgvgWGC73i8nIiJi3bT1pBDbj7d8ltq+GBj4f7AQEREbjXanHPdt+XETmhFbu6O77n2dDzxt+1/XZf8e+ns5cDWwHzDR9j/0Rr8REbFhaTeUvtyy/AKwBDiu98tZJ88CnwL2Lp+IiNgItftw4vfbPrR83mb7dOC5dg8i6VxJD0q6Hdi9tO0qaZqkOZJmSNqjtE+UdKmkOyQtljS+tE+SNK6lz4mSxtv+k+3baYKtnVqOkjRX0gJJN5e2/SXdKWleOW5XjXtJulvSfEn3lOdYIum9Le1flzSofCZKulfSQkkf6+HYp0uaLWn2imXdn/UcERHro91Au7rNtr8iaQxwAjAaeDvN1CDABOBDtscAZwOXt+w2DDgIeAdwQWmbTBkVStocOByY2mb9XbUMBf4deLftUTQ3twDcDxxs+/XAp4EvlPYzgEtsj6aZZv2NpD2B44E3lfYVwInl+w23vbftfYBvdT++7Qm2x9oeO2irPHglIqI3rXbKsYya9gKGSPpfLau2pbnbsR0HAz+0vaz0OaXseyBwlaSu7Qa37HOt7ZXAfZJ2KG3XA5dIGgwcBUy3/UybNXR5Q9lvCYDtJ0r7EODKMgIzsFlpvxM4V9KOwDW2H5J0ODAGmFVq3xJ4FPgRsIuky2iC9sa1rC0iItbDmq6h7U4zSnopcHRL+x+Bv1uP424CPFlGOD1Z3rIsANvPSroVOJJmhDRpPY7f3WeBn9p+l6QRwK3lmN+TdBfNHZ3/JemDpZ4rbX+yeyeSRpX6zqAZTZ7WizVGRMRqrHbK0fZ1tk8F3mH71JbPh223+z606cAxkraUtA1NMC4Dlkg6FkCNUW30NRk4lWbUN63N47f6GXCIpJ3Lcbv+lm4IsLQsn9K1saRdgMW2LwWuA14H3AyMl/SKrj4k7SRpe2AT2z8AzgNa7wyNiIg+1u5djvMknUUz/fjnqUbbaxyB2J4raTKwgGZqblZZdSJwhaTzaKb4JpVtVudG4NvAdbb/fFOKpIdppkE3l3QMcITt+3qo5XeSTgeukbRJqedtwJdophzP48XX5Y4DTpL0PPA/wBdsP1G2u7H08TxwFvAM8K3SBvBXI7iIiOg77b7g8yqaGyfeA3yGJox+bvsjfVtevfKCz4gYaDb0F3y2e5fjbrY/BfypPKh4HHBAbxUYERGxvtqdcny+/PNJSXvTTL+9om9K6h3lZo7B3ZpPsr2wE/VERETfajfQJkh6Gc0TOaYAW9P8vdaAZTsjyIiIjUi770P7Rlm8DcgrYyIiYsBp9+HEO9A8PeOVtv9G0muBN9r+jz6trmL7DB/C7A3gAmxExIai3ZtCJgI3AK8sPz8IfLQvCoqIiFgX7Qba9ra/D6wEsP0CzTMMIyIiBoR2A+1P5b1jBpD0BiCPi4+IiAGj3bsc/5Hm7sZdJc0EhgLj+6yqiIiItbSmp+2/2vZ/l8dXvZnmYcUCHrD9/Or2jYiI6E9rmnK8tmV5su1Ftu9NmEVExECzpkBTy3L+/iwiIgasNQWaV7EcERExoKzpppBRkv5AM1LbsixTfrbtbfu0uoiIiDatNtBsD+qvQiIiItZHu3+HFhERMaAl0CIiogoJtIiIqEICLSIiqpBAi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCu2+sjl62cOlTjDhnaqfLiIiN1MMXjOt0Cb0uI7SIiKhCAi0iIqqQQIuIiCok0CIiogoJtIiIqEICLSIiqpBAi4iIKvR7oEk6X9LZfdDvqyU93Rd9R0TEwFfTCO0rwPWdLiIiIjqjXwJN0rmSHpR0O7B7adtV0jRJcyTNkLRHaZ8o6VJJd0haLGl8aZ8kaVxLnxNb1h0DLAEWtVHL+yTdI2mBpG+XtqMl3SVpnqSfSNqhtL9Z0vzymSdpm9L+T5JmlX7+pbS9RNLU0u+9ko7vxVMYERFr0OePvpI0BjgBGF2ONxeYA0wAzrD9kKQDgMuBw8puw4CDgD2AKcDVwGTgOGCqpM2Bw4EzJW0N/DPwNmC1042S9gLOAw60/Zik7cqq24E32LakDwCfAD5e+jvL9sxynGclHQGMBPYHBEyRdAgwFHjE9rhyrCE9HP904HSAQdsObfcURkREG/rjWY4HAz+0vQxA0hRgC+BA4CpJXdsNbtnnWtsrgfu6Rks004mXSBoMHAVMt/2MpH8F/s320y19rcphwFW2HwOw/URp3xGYLGkYsDnNaA9gJvAVSd8FrrH9mxJoRwDzyjZb0wTcDODLki4Efmx7RveD255AE+QMHjbSayo2IiLa16mHE28CPGl79CrWL29ZFoDtZyXdChwJHA9MKusPAMZL+hLwUmClpGdtf3Ut6rkM+IrtKZLeApxfjnmBpKnA24GZko4s9XzR9te7dyJp37Lt5yTdbPsza1FDRESsh/64hjYdOEbSluUa1NHAMmCJpGMB1BjVRl+TgVNpRn3TAGwfbHuE7RHAxcAXVhNmtwDHSnp5OW7XlOMQYGlZPrlrY0m72l5o+0JgFs0U6A3AaWUKEknDJb1C0iuBZba/A1wE7NvG94mIiF7S5yM023MlTQYWAI/SBAPAicAVks4DNqMZcS1YQ3c3At8GrrP93DrUskjS54HbJK2gmTY8hWZEdpWk39OE3s5ll49KOhRYSXPDyfW2l0vaE7izTHE+DbwX2A24SNJK4HngzLWtLyIi1p3sXMrphMHDRnrYyRd3uoyI2EhtqO9DkzTH9tie1tX0d2gREbERq/KN1eUa2c09rDrc9uP9XU9ERPS9KgOthNaq7qCMiIgKZcoxIiKqUOUIbUOwz/AhzN5AL8pGRAxEGaFFREQVEmgREVGFBFpERFQhgRYREVVIoEVERBUSaBERUYUEWkREVCGBFhERVUigRUREFRJoERFRhQRaRERUIYEWERFVSKBFREQVEmgREVGFBFpERFQhgRYREVVIoEVERBUSaBERUYUEWkREVCGBFhERVUigRUREFTbtdAEbq4VLn2LEOVM7XUbEBuPhC8Z1uoQY4DJCi4iIKiTQIiKiCgm0iIioQgItIiKqkECLiIgqJNAiIqIKCbSIiKhCAi0iIqqQQOslkiZKGt/pOiIiNlYJtIiIqEKfBZqkl0iaKmmBpHslHS9pjKTbJM2RdIOkYWXbv5M0q2z7A0lblfZjy74LJE0vbVtI+pakhZLmSTq0tJ8i6RpJ0yQ9JOlLq6ntWElfKcsfkbS4LO8iaWZZXlWtu5ZjzJE0Q9IePfT/2TJiG9St/XRJsyXNXrHsqd44zRERUfTlCO0o4BHbo2zvDUwDLgPG2x4DfBP4fNn2Gtv72R4F/Bx4f2n/NHBkaf/b0nYWYNv7AP8buFLSFmXdaOB4YB/geEmvWkVtM4CDy/LBwOOShpfl6ZI2W02tE4APlfazgctbO5Z0ETAUONX2itZ1tifYHmt77KCthqz+7EVExFrpy4cTLwS+LOlC4MfA74G9gZskAQwCflu23VvS54CXAlsDN5T2mcBESd8HriltB9GEDbbvl/Qr4DVl3c22nwKQdB+wE/Dr7oXZ/h9JW0vaBngV8D3gEJpAuwbYvadaJW0NHAhcVdoBBrd0/SngLtunr92pioiI9dVngWb7QUn7Am8HPgfcAiyy/cYeNp8IHGN7gaRTgLeUPs6QdAAwDpgjacwaDru8ZXkFq/9+dwCnAg/QjNhOA94IfBx4dU+1StoWeNL26FX0OQsYI2k720+sodaIiOhFfXkN7ZXAMtvfAS4CDgCGSnpjWb+ZpL3K5tvQjIA2A05s6WNX23fZ/jTwO5rR1IyubSS9hiZ8HliHEmfQTBlOB+YBhwLLywjvgZ5qtf0HYImkY0u7JI1q6XMacAEwtYz+IiKin/TllOM+wEWSVgLPA2cCLwCXShpSjn0xsIgyVUcTWnfRBBxl/5GAgJuBBcD9wBWSFpb+TrG9vGUKsF0zaAJyuu0Vkn5d+sb2c+UW/J5qPbEc/zxgM2BSqYuy71UlzKZIervtZ9a2sIiIWHuy3ekaNkqDh430sJMv7nQZERuMvOAzACTNsT22p3X5O7SIiKhCX045DgiS7uLFdyICnGR7YSfqiYiIvlF9oNk+oNM1RERE38uUY0REVKH6EdpAtc/wIczORe6IiF6TEVpERFQhgRYREVVIoEVERBUSaBERUYUEWkREVCGBFhERVUigRUREFRJoERFRhQRaRERUIYEWERFVyPvQOkTSH1m3N21vDLYHHut0EQNUzs2q5dysWk3nZifbQ3takWc5ds4Dq3pJ3cZO0uycm57l3Kxazs2qbSznJlOOERFRhQRaRERUIYHWORM6XcAAlnOzajk3q5Zzs2obxbnJTSEREVGFjNAiIqIKCbSIiKhCAq0PSDpK0gOSfiHpnB7WD5Y0uay/S9KIlnWfLO0PSDqyP+vuD+t6biSNkPSMpPnl87X+rr2vtXFuDpE0V9ILksZ3W3eypIfK5+T+q7rvred5WdHyOzOl/6ruH22cm3+UdJ+keyTdLGmnlnX1/c7YzqcXP8Ag4JfALsDmwALgtd22+Xvga2X5BGByWX5t2X4wsHPpZ1Cnv9MAOTcjgHs7/R06fG5GAK8D/hMY39K+HbC4/PNlZfllnf5OnT4vZd3Tnf4OHT43hwJbleUzW/57qvJ3JiO03rc/8Avbi20/B0wC3tltm3cCV5blq4HDJam0T7K93PYS4Belv1qsz7mp3RrPje2Hbd8DrOy275HATbafsP174CbgqP4ouh+sz3mpXTvn5qe2l5UffwbsWJar/J1JoPW+4cCvW37+TWnrcRvbLwBPAS9vc98N2fqcG4CdJc2TdJukg/u62H62Pv/ua/69Wd/vtoWk2ZJ+JumY3i2t49b23LwfuH4d990g5NFXsaH4LfBq249LGgNcK2kv23/odGExoO1ke6mkXYBbJC20/ctOF9XfJL0XGAu8udO19KWM0HrfUuBVLT/vWNp63EbSpsAQ4PE2992QrfO5KdOwjwPYnkNz7eA1fV5x/1mff/c1/96s13ezvbT8czFwK/D63iyuw9o6N5LeCpwL/K3t5Wuz74Ymgdb7ZgEjJe0saXOaGxu63101Bei6q2g8cIubK7VTgBPKnX47AyOBu/up7v6wzudG0lBJgwDK/22PpLmQXYt2zs2q3AAcIellkl4GHFHaarDO56Wcj8FleXvgTcB9fVZp/1vjuZH0euDrNGH2aMuqOn9nOn1XSo0f4O3AgzSjiHNL22dofqkAtgCuornp425gl5Z9zy37PQD8Tae/y0A5N8C7gUXAfGAucHSnv0sHzs1+NNc6/kQzol/Usu9p5Zz9Aji1099lIJwX4EBgIc3dfwuB93f6u3Tg3PwE+H/lv5v5wJSaf2fy6KuIiKhCphwjIqIKCbSIiKhCAi0iIqqQQIuIiCok0CIiogoJtIgOkbSDpO9JWixpjqQ7Jb2rrBsr6dI2+rhjbdr7Snkbwnv685gR3eW2/YgOKA9cvgO40vbXSttONH8/dFlHi1tL5YkuBwFn235Hp+uJjVdGaBGdcRjwXFeYAdj+VVeYSXqLpB+X5fMlfVPSrWU09+GufSQ93VPnXe2ln9skXVf2vUDSiZLulrRQ0q5lu4mSvlYe5PugpHeU9i0kfatsO0/SoaX9FElTJN0C3AxcABxc3jv2sTJim1HeUzZX0oEt9dwq6WpJ90v6btfbFCTtJ+kOSQtKfdtIGiTpIkmzyju9Ptjb/yKiHnk4cURn7EXzxJN27UHzbqttgAckXWH7+Tb3HQXsCTxB87iwb9jeX9JHgA8BHy3bjaB5JcmuwE8l7QacBdj2PpL2AG6U1PUMzX2B19l+QtJbaBmhSdoKeJvtZyWNBP4vzcNxoXme4l7AI8BM4E2S7gYmA8fbniVpW+AZmifEP2V7v/IYq5mSbnTzeqWIF0mgRQwAkv4PzbTdc7b362GTqW4eLLtc0qPADjSPe2rHLNu/Lcf5JXBjaV9IE5Jdvm97JfCQpMU0IXoQcBmA7fsl/Yq/PBT6JttPrOKYmwFflTQaWMGLHyR9t+3flHrm0wTpU8Bvbc8qx/pDWX8E8Dr95U3UQ2ie45lAi7+SQIvojEU0z6cEwPZZ5QG6s1ex/fKW5RWs3X+7rfuubPl5Zbd+ul9QX9MF9j+tZt3HaJ4hOIrm0sazq6hnTd9FwIdsb/gPzo0+l2toEZ1xC83LJ89saduqU8UUx0rapFxX24XmAdkzgBMBylTjq0t7d3+kmQ7tMoRmxLUSOAkYtIZjPwAMk7RfOdY25WaTG4AzJW3WVYOkl6zrF4y6ZYQW0QG2reYNyv8m6RPA72hGPP/cwbL+m+YNB9sCZ5TrX5cDV0haCLwAnGJ7ebmPo9U9wApJC4CJwOXADyS9D5jG6kdz2H5O0vHAZZK2pLl+9lbgGzRTknPLzSO/A2p783T0kty2HxFImgj82PbVna4lYl1lyjEiIqqQEVpERFQhI7SIiKhCAi0iIqqQQIuIiCok0CIiogoJtIiIqML/B4KZOD+b/I3kAAAAAElFTkSuQmCC\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "rjXZdsVZ1EuY"
      },
      "source": [
        "#Making predictions\n",
        "\n",
        "y_pred = model.predict(X_train)\n",
        "\n",
        "submission = pd.DataFrame(y_pred, columns=['total_cases'], index=X_train.index)\n",
        "\n",
        "submission.to_csv('2000_to_2009_submission.csv')"
      ],
      "execution_count": 19,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "nkZL_VxN2DIm",
        "outputId": "016aa381-4dc9-47c4-be75-90ab4bde4329",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 373
        }
      },
      "source": [
        "submission.tail(10)"
      ],
      "execution_count": 20,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>total_cases</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>week_start_date</th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>2009-04-23</th>\n",
              "      <td>5</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-04-30</th>\n",
              "      <td>4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-05-07</th>\n",
              "      <td>4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-05-14</th>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-05-21</th>\n",
              "      <td>1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-05-28</th>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-04</th>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-11</th>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-18</th>\n",
              "      <td>5</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2009-06-25</th>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "                 total_cases\n",
              "week_start_date             \n",
              "2009-04-23                 5\n",
              "2009-04-30                 4\n",
              "2009-05-07                 4\n",
              "2009-05-14                 0\n",
              "2009-05-21                 1\n",
              "2009-05-28                 2\n",
              "2009-06-04                 3\n",
              "2009-06-11                 3\n",
              "2009-06-18                 5\n",
              "2009-06-25                 2"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 20
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "XuhJNvCZzg0R"
      },
      "source": [
        "#Visulizations\n",
        "\n"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "FPTR_mBQ73K2",
        "outputId": "44aab0b1-fc65-44fd-cad6-b60e2f6f708f",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Dropping 'season_week' since I do not need it.\n",
        "X_train.drop('season_week', axis=1, inplace=True)"
      ],
      "execution_count": 21,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "/usr/local/lib/python3.6/dist-packages/pandas/core/frame.py:4174: SettingWithCopyWarning: \n",
            "A value is trying to be set on a copy of a slice from a DataFrame\n",
            "\n",
            "See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy\n",
            "  errors=errors,\n"
          ],
          "name": "stderr"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "1FdG7DK1Q99j",
        "outputId": "ab0144e7-58d8-442d-fd7d-683f9abbdc40",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "#Ceating a new model with XGBRegressor\n",
        "\n",
        "from xgboost import XGBRegressor\n",
        "\n",
        "model_boost = XGBRegressor(n_estimators=20, random_state=42)\n",
        "model_boost.fit(X_train, y_train);"
      ],
      "execution_count": 22,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "[11:03:57] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "M3tpXLhcA5Bi"
      },
      "source": [
        "import matplotlib.pyplot as plt"
      ],
      "execution_count": 23,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "uJcp-PU7bnsM",
        "outputId": "085ca0b3-033d-4455-832a-60051a4b7501",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 225
        }
      },
      "source": [
        "X_train.head()"
      ],
      "execution_count": 24,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>denv1_cases</th>\n",
              "      <th>denv2_cases</th>\n",
              "      <th>denv3_cases</th>\n",
              "      <th>denv4_cases</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>week_start_date</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>1990-04-30</th>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1990-05-07</th>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1990-05-14</th>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1990-05-21</th>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1990-05-28</th>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "                 denv1_cases  denv2_cases  denv3_cases  denv4_cases\n",
              "week_start_date                                                    \n",
              "1990-04-30                 0            0            0            0\n",
              "1990-05-07                 0            0            0            0\n",
              "1990-05-14                 0            0            0            0\n",
              "1990-05-21                 0            0            0            0\n",
              "1990-05-28                 0            0            0            0"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 24
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "vxjDq1-XAak_"
      },
      "source": [
        "###First Visual\n",
        "\n",
        "This visual shows us all the strains of the virus based on when the week had started and how many cases there were on that week"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "i1jo58hRIzX9",
        "outputId": "28e3f7c4-885e-4c2e-e198-f103faed6348",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 606
        }
      },
      "source": [
        "fig, axes = plt.subplots(nrows=4, ncols=1, figsize=(10,10));\n",
        "X_train[['denv1_cases']].plot(ax=axes[0], color=['#667e2c']);\n",
        "X_train[['denv2_cases']].plot(ax=axes[1], color=['#d2bd0a']);\n",
        "X_train[['denv3_cases']].plot(ax=axes[2], color=['#10a674']);\n",
        "X_train[['denv4_cases']].plot(ax=axes[3], color=['#580f41']);"
      ],
      "execution_count": 25,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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cnJyRHlKMEopcnJy4rYEigIlCIIgCAlClKdjg8b8DqJACYIgCIIgxIkoUIIgCIIgCHEiCpQgCIIgCNxzzz088sgjzdbesmXLOOmkkzjppJMYM2YM77zzTrO1fSwgo/AEQRAEIcHcuWIu60oPNGubozv14i/jpjdrm/EwatQo8vLycLlcFBQUMGbMGC699FJcrvaheogFShAEQRCOU+6//36GDh3KGWecwZYtWwDYsWMHF154IePGjWPy5Mls3rwZgOuuu45f/OIXTJo0iYEDBzJnzhwAZs6cyf/+979Am9dddx1z5swhPT09oCzV1NQ0GKj98ssvc+KJJzJmzBiuvfZaAN5//30mTpzI2LFjOffcczl48CAAX375ZcC6NXbsWMrLywF4+OGHmTBhAieeeCJ33303AJWVlVx88cWMGTOGUaNGMXv27OYRnta61f7GjRunBUEQhKbT6T+/0Z3+85tEd0NoAhs3bkzo8fPy8vSoUaN0ZWWlLisr04MGDdIPP/ywnjp1qt66davWWuslS5bos88+W2ut9axZs/SVV16pvV6v3rBhgx40aJDWWuu3335bf//739daa11bW6tzc3N1VVVVYP8RI0bojIwM/fbbb0fsy/r16/WQIUP0oUOHtNZaFxcXa621PnLkiPb5fFprrZ999ll96623aq21vuSSS/SiRYu01lqXl5drt9ut582bp3/0ox9pn8+nvV6vvvjii/WXX36p58yZo3/4wx8GjlVaWmrbB7vfA8jTEXSa9mFHEwRBEAQhLhYuXMi3vvUt0tPTAbjsssuoqanh66+/5qqrrgrUq62tDSxffvnlOBwORowYEbAGTZs2jVtuuYXa2lo+/vhjpkyZQlpaGgATJ05kw4YNbNq0iVmzZjFt2jRSU1PD+vL5559z1VVX0aVLFwA6d+4MGMlGZ8yYQUFBAXV1dYFEl6effjq33norV199NVdccQW5ubl88sknfPLJJ4wdOxaAiooKtm3bxuTJk/n1r3/N7bffziWXXMLkyZObRX7iwhMEQRAEAQCfz0enTp1YvXp14G/Tpk2B7SkpKYFlw0BjTINy1llnMW/ePGbPns2MGTPC2h0+fDgdOnRg/fr1cfXn5ptv5qabbmLdunX861//CiS7vOOOO3juueeorq7m9NNPZ/PmzWitufPOOwP93r59OzfccANDhw5l5cqV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\n",
            "text/plain": [
              "<Figure size 720x720 with 4 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "_3nnjz-6O4ao",
        "outputId": "275d1404-7150-4e35-adb5-9b622d470300",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "!pip install pdpbox"
      ],
      "execution_count": 26,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Requirement already satisfied: pdpbox in /usr/local/lib/python3.6/dist-packages (0.2.0)\n",
            "Requirement already satisfied: joblib in /usr/local/lib/python3.6/dist-packages (from pdpbox) (0.17.0)\n",
            "Requirement already satisfied: matplotlib>=2.1.2 in /usr/local/lib/python3.6/dist-packages (from pdpbox) (3.2.2)\n",
            "Requirement already satisfied: scipy in /usr/local/lib/python3.6/dist-packages (from pdpbox) (1.4.1)\n",
            "Requirement already satisfied: psutil in /usr/local/lib/python3.6/dist-packages (from pdpbox) (5.4.8)\n",
            "Requirement already satisfied: scikit-learn in /usr/local/lib/python3.6/dist-packages (from pdpbox) (0.22.2.post1)\n",
            "Requirement already satisfied: numpy in /usr/local/lib/python3.6/dist-packages (from pdpbox) (1.18.5)\n",
            "Requirement already satisfied: pandas in /usr/local/lib/python3.6/dist-packages (from pdpbox) (1.1.4)\n",
            "Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.2->pdpbox) (2.4.7)\n",
            "Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.2->pdpbox) (0.10.0)\n",
            "Requirement already satisfied: python-dateutil>=2.1 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.2->pdpbox) (2.8.1)\n",
            "Requirement already satisfied: kiwisolver>=1.0.1 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.2->pdpbox) (1.3.1)\n",
            "Requirement already satisfied: pytz>=2017.2 in /usr/local/lib/python3.6/dist-packages (from pandas->pdpbox) (2018.9)\n",
            "Requirement already satisfied: six in /usr/local/lib/python3.6/dist-packages (from cycler>=0.10->matplotlib>=2.1.2->pdpbox) (1.15.0)\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "V5Wg97Dv8xAk",
        "outputId": "3e8177f6-ef1f-4403-8030-6be90d967ef0",
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "source": [
        "X_val.drop('season_week', axis=1, inplace=True)"
      ],
      "execution_count": 27,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "/usr/local/lib/python3.6/dist-packages/pandas/core/frame.py:4174: SettingWithCopyWarning: \n",
            "A value is trying to be set on a copy of a slice from a DataFrame\n",
            "\n",
            "See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy\n",
            "  errors=errors,\n"
          ],
          "name": "stderr"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "mt5UxfMXBFIP"
      },
      "source": [
        "###Second Visual"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "qQvBu8PmSo9V",
        "outputId": "94907e0e-3c2f-4acf-979c-7ea91a2569f8",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 648
        }
      },
      "source": [
        "from pdpbox.pdp import pdp_interact, pdp_interact_plot\n",
        "\n",
        "features = ['denv4_cases', 'denv2_cases']\n",
        "\n",
        "interact = pdp_interact(\n",
        "    model= model_boost,\n",
        "    dataset=X_val,\n",
        "    model_features=X_val.columns,\n",
        "    features=features\n",
        ")\n",
        "\n",
        "pdp_interact_plot(interact, plot_type='grid', feature_names=features);"
      ],
      "execution_count": 31,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "findfont: Font family ['Arial'] not found. Falling back to DejaVu Sans.\n",
            "findfont: Font family ['Arial'] not found. Falling back to DejaVu Sans.\n",
            "findfont: Font family ['Arial'] not found. Falling back to DejaVu Sans.\n",
            "findfont: Font family ['Arial'] not found. Falling back to DejaVu Sans.\n"
          ],
          "name": "stderr"
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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mFvbiIiI7InN9wmXfej/Wg11ISIiohpm888QExER0Z2DQYCIiMiOMQgQERHZMQYBIiIiO8YgQEREZMcYBIiIiOwYgwAREZEdYxAgIiKyYwwCREREdoxBgIiIyI4xCBAREdkxBgEiIiI7xiBARERkxxgEiIiI7BiDABERkR1jECAiIrJjDAJERER2jEGAiIjIjjEIEBER2TEGASIiIjvGIEBERGTHGASIiIjsGIMAERGRHRMURantOlSHO7JRRET0rwk3W/HMgs+q9LNj06SBN93Xf4lDbVegOjzmPDi6tutQF6l8vLEzcUlk98CX2X822pm4JLJbxDT2m412nZkT2bXNW+w3G+35fWZku/4L2G//wKGtk2q7Cv85vDRARERkxxgEiIiI7BiDABERkR1jECAiIrJjDAJERER2jEGAiIjIjjEIEBER2TEGASIiIjvGIEBERGTHGASIiIjsGIMAERGRHWMQICIismMMAkRERHaMQYCIiMiO3ZE/Q0xERPRfJ0lSOIAtFRaFAJghy/KSsvUTASwAUE+W5cxKZVsA+BCAGwAzgNmyLFfc1m3jiAAREVEtkGU5VpblFrIstwAQCaAIwNcAIElSAICuABJvUrwIwBBZliMAdAOwRJIkj39SD44IEBERAUhIzKrN3UsALsmynFD2fDGAKQC+udGLZVk+X+FxqiRJVwDUA5Br644ZBIiIiAA0V9yrdHtr164dAWBEhUUro6KiVt7k5QMAbAIASZL6AEiRZflPSZJuuR9JktoA0AC49E/qySBARERUDco+9G/2wf8XSZI0AHoDmCpJkjOAabBeFrglSZIaAvgUwFBZli3/pJ6cI0BERFS7ugM4LstyBoAmABoD+FOSpHgA/gCOS5LkW7mQJEluAH4A8Losy0f+6c45IkBERFS7nkHZZQFZlk8BqF++oiwMtL7BXQMaWCcWbpBl+ct/s3MGASIioloiSZIOwKMARt7Ga1sDeFGW5ecB/A9ARwDekiQNK3vJMFmW/7C1DgwCREREtUSWZT0A779ZH1zh8TEAz5c93ghgY1XUgXMEiIiI7BiDABERkR1jECAiIrJjDAJERER2jJMF/6GFP00PDbrb33nXur1XVr++Oc3dx1WcueXlEAeNg0oUVcLS8esSYo9eMtyo7NL9b4anx18tnjNkeYKLh041b+fUMLPRpGi0GtW6t75M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\n",
            "text/plain": [
              "<Figure size 540x684 with 3 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "24lBmPU7AxNn"
      },
      "source": [
        "###Third Visual\n",
        "\n",
        "This visual just tells us the feature importance based on the moodel_boost using a XGGRegeressor."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "nKsfAPuGTsqV",
        "outputId": "2e889e64-dac6-456b-d296-70a3df7af752",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 295
        }
      },
      "source": [
        "from numpy import loadtxt\n",
        "from xgboost import XGBClassifier\n",
        "from xgboost import plot_importance\n",
        "from matplotlib import pyplot\n",
        "\n",
        "\n",
        "\n",
        "plot_importance(model_boost, color = '#005249')\n",
        "pyplot.show()"
      ],
      "execution_count": 29,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    }
  ]
})
