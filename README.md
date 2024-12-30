{
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "y2VgPk2mTThF"
      },
      "source": [
        "# **Exploratory Data Analysis (EDA) with Pandas in Banking**\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "jkRBtAnQTThK"
      },
      "source": [
        "The purpose of this project is to master the exploratory data analysis (EDA) in banking with Pandas framework.\n",
        "\n",
        "Goals of the Project:\n",
        "\n",
        "1.  Explore a banking dataset with Pandas framework.\n",
        "2.  Build pivot tables.\n",
        "3.  Visualize the dataset with various plot types.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "CHwOXFUpTThK"
      },
      "source": [
        "## Outline\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "bHSc4iksTThP"
      },
      "source": [
        "*   Materials and methods\n",
        "*   General part\n",
        "    *   Libraries import\n",
        "    *   Dataset exploration\n",
        "    *   Pivot tables\n",
        "    *   Visualization in Pandas\n",
        "*   Tasks\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "S4t5rpwITThQ"
      },
      "source": [
        "***\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "KoNAvKmglBm-"
      },
      "source": [
        "## Materials and methods\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ZOgyr5RSlI40"
      },
      "source": [
        "The data that we are going to use for this is a subset of an open source Bank Marketing Data Set from the UCI ML repository: https://archive.ics.uci.edu/ml/citation_policy.html.\n",
        "\n",
        "> This dataset is publicly available for research. The details are described in \\[Moro et al., 2014].\n",
        "\n",
        "During the work, the task of preliminary analysis of a positive response (term deposit) to direct calls from a bank is to solve. In essence, the task is a matter of bank scoring, i.e. according to the characteristics of a client (potential client), their behavior is predicted (loan default, a wish to make a deposit, etc.).\n",
        "\n",
        "In this project, we will try to give answers to a set of questions that may be relevant when analyzing banking data:\n",
        "\n",
        "1.  What is the share of clients attracted in our source data?\n",
        "2.  What are the mean values of numerical features among the attracted clients?\n",
        "3.  What is the average call duration for the attracted clients?\n",
        "4.  What is the average age among the attracted and unmarried clients?\n",
        "5.  What is the average age and call duration for different types of client employment?\n",
        "\n",
        "In addition, we will make a visual analysis in order to plan marketing banking campaigns more effectively.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "xS8UOiQOTThR"
      },
      "source": [
        "## Libraries import\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "H6YFQWnQHKui"
      },
      "source": [
        "Download data using a URL.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 3,
      "metadata": {
        "id": "bN5NPujBTThV",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "edb28c29-8f65-4901-e805-9589fd11f54e"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "--2022-04-19 05:12:45--  https://archive.ics.uci.edu/ml/machine-learning-databases/00222/bank-additional.zip\n",
            "Resolving archive.ics.uci.edu (archive.ics.uci.edu)... 128.195.10.252\n",
            "Connecting to archive.ics.uci.edu (archive.ics.uci.edu)|128.195.10.252|:443... connected.\n",
            "HTTP request sent, awaiting response... 200 OK\n",
            "Length: 444572 (434K) [application/x-httpd-php]\n",
            "Saving to: ‘bank-additional.zip’\n",
            "\n",
            "bank-additional.zip 100%[===================>] 434.15K  1.74MB/s    in 0.2s    \n",
            "\n",
            "2022-04-19 05:12:46 (1.74 MB/s) - ‘bank-additional.zip’ saved [444572/444572]\n",
            "\n"
          ]
        }
      ],
      "source": [
        "!wget https://archive.ics.uci.edu/ml/machine-learning-databases/00222/bank-additional.zip"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "-BnB2tiSZh4R"
      },
      "source": [
        "Alternative URL for the dataset downloading.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 4,
      "metadata": {
        "id": "ORfD1EUiZuLK",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "4004f5ae-504a-4bae-e216-6c6e1b17a3c7"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "--2022-04-19 05:12:54--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/EDA_Pandas_Banking_L1/bank-additional.zip\n",
            "Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 198.23.119.245\n",
            "Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|198.23.119.245|:443... connected.\n",
            "HTTP request sent, awaiting response... 200 OK\n",
            "Length: 444572 (434K) [application/zip]\n",
            "Saving to: ‘bank-additional.zip.1’\n",
            "\n",
            "bank-additional.zip 100%[===================>] 434.15K  2.03MB/s    in 0.2s    \n",
            "\n",
            "2022-04-19 05:12:55 (2.03 MB/s) - ‘bank-additional.zip.1’ saved [444572/444572]\n",
            "\n"
          ]
        }
      ],
      "source": [
        "!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/EDA_Pandas_Banking_L1/bank-additional.zip"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 5,
      "metadata": {
        "id": "iZKbsroFTThY"
      },
      "outputs": [],
      "source": [
        "!unzip -o -q bank-additional.zip"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "eGH5DhdLHmOp"
      },
      "source": [
        "Importing the libraries necessary for this project. We can add some aliases to make the libraries easier to use in our code and set a default figure size for further plots.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 6,
      "metadata": {
        "id": "jdVcijxmTTha"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import matplotlib.pyplot as plt\n",
        "import numpy as np\n",
        "\n",
        "%matplotlib inline\n",
        "plt.rcParams[\"figure.figsize\"] = (8, 6)\n",
        "\n",
        "import warnings\n",
        "warnings.filterwarnings('ignore')"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "evtbog-C13Z2"
      },
      "source": [
        "Further specify the value of the `precision` parameter equal to 2 to display two decimal signs (instead of 6 as default).\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 7,
      "metadata": {
        "id": "nwMoaJLV13Z3"
      },
      "outputs": [],
      "source": [
        "pd.set_option(\"precision\", 2)\n",
        "pd.options.display.float_format = '{:.2f}'.format"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "SbmrZguMTThd"
      },
      "source": [
        "## Dataset exploration\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "EvMGO3m4TThd"
      },
      "source": [
        "In this section we will explore the sourse dataset.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "lJ-GKs1J13Zz"
      },
      "source": [
        "Let's read the data and look at the first 5 rows using the `head` method. The number of the output rows from the dataset is determined by the `head` method parameter.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 8,
      "metadata": {
        "id": "wamAf3HLm_FS",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "outputId": "571ac87e-b5a4-4de7-9104-12ff2a718c97"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   age        job  marital    education  default housing loan    contact  \\\n",
              "0   56  housemaid  married     basic.4y       no      no   no  telephone   \n",
              "1   57   services  married  high.school  unknown      no   no  telephone   \n",
              "2   37   services  married  high.school       no     yes   no  telephone   \n",
              "3   40     admin.  married     basic.6y       no      no   no  telephone   \n",
              "4   56   services  married  high.school       no      no  yes  telephone   \n",
              "\n",
              "  month day_of_week  ...  campaign  pdays  previous     poutcome emp.var.rate  \\\n",
              "0   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "1   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "2   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "3   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "4   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "\n",
              "   cons.price.idx  cons.conf.idx  euribor3m  nr.employed   y  \n",
              "0           93.99         -36.40       4.86      5191.00  no  \n",
              "1           93.99         -36.40       4.86      5191.00  no  \n",
              "2           93.99         -36.40       4.86      5191.00  no  \n",
              "3           93.99         -36.40       4.86      5191.00  no  \n",
              "4           93.99         -36.40       4.86      5191.00  no  \n",
              "\n",
              "[5 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-a1ea7fe8-2b63-485f-8032-c4f605e326e9\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>56</td>\n",
              "      <td>housemaid</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.4y</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>57</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>unknown</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>37</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>40</td>\n",
              "      <td>admin.</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.6y</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>56</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-a1ea7fe8-2b63-485f-8032-c4f605e326e9')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-a1ea7fe8-2b63-485f-8032-c4f605e326e9 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-a1ea7fe8-2b63-485f-8032-c4f605e326e9');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 8
        }
      ],
      "source": [
        "df = pd.read_csv('bank-additional/bank-additional-full.csv', sep = ';')\n",
        "df.head(5)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "NjzxXtUp13Z3"
      },
      "source": [
        "### Let's look at the dataset size, feature names and their types\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "53xc7fWwoOMD",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 317
        },
        "outputId": "0cfc52cf-1d2a-4328-d920-e1b90bb19703"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       age          job  marital            education default housing loan  \\\n",
              "41183   73      retired  married  professional.course      no     yes   no   \n",
              "41184   46  blue-collar  married  professional.course      no      no   no   \n",
              "41185   56      retired  married    university.degree      no     yes   no   \n",
              "41186   44   technician  married  professional.course      no      no   no   \n",
              "41187   74      retired  married  professional.course      no     yes   no   \n",
              "\n",
              "        contact month day_of_week  ...  campaign  pdays  previous  \\\n",
              "41183  cellular   nov         fri  ...         1    999         0   \n",
              "41184  cellular   nov         fri  ...         1    999         0   \n",
              "41185  cellular   nov         fri  ...         2    999         0   \n",
              "41186  cellular   nov         fri  ...         1    999         0   \n",
              "41187  cellular   nov         fri  ...         3    999         1   \n",
              "\n",
              "          poutcome emp.var.rate  cons.price.idx  cons.conf.idx  euribor3m  \\\n",
              "41183  nonexistent        -1.10           94.77         -50.80       1.03   \n",
              "41184  nonexistent        -1.10           94.77         -50.80       1.03   \n",
              "41185  nonexistent        -1.10           94.77         -50.80       1.03   \n",
              "41186  nonexistent        -1.10           94.77         -50.80       1.03   \n",
              "41187      failure        -1.10           94.77         -50.80       1.03   \n",
              "\n",
              "       nr.employed    y  \n",
              "41183      4963.60  yes  \n",
              "41184      4963.60   no  \n",
              "41185      4963.60   no  \n",
              "41186      4963.60  yes  \n",
              "41187      4963.60   no  \n",
              "\n",
              "[5 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-164c87a3-0de6-4ade-be0e-d3700ed27c00\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>41183</th>\n",
              "      <td>73</td>\n",
              "      <td>retired</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>41184</th>\n",
              "      <td>46</td>\n",
              "      <td>blue-collar</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>41185</th>\n",
              "      <td>56</td>\n",
              "      <td>retired</td>\n",
              "      <td>married</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>2</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>41186</th>\n",
              "      <td>44</td>\n",
              "      <td>technician</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>41187</th>\n",
              "      <td>74</td>\n",
              "      <td>retired</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>3</td>\n",
              "      <td>999</td>\n",
              "      <td>1</td>\n",
              "      <td>failure</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-164c87a3-0de6-4ade-be0e-d3700ed27c00')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-164c87a3-0de6-4ade-be0e-d3700ed27c00 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-164c87a3-0de6-4ade-be0e-d3700ed27c00');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 7
        }
      ],
      "source": [
        "df.shape\n",
        "df.tail(5)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "HtO5KNTV13Z5"
      },
      "source": [
        "The dataset contains 41188 objects (rows), for each of which 21 features are set (columns), including 1 target feature (`y`).\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "KVOmrfNH3pRs"
      },
      "source": [
        "### Attributing information\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "TSTqzHlbKWoa"
      },
      "source": [
        "Output the column (feature) names:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "3uuAnHe3nvCh",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "e84a01fa-9955-4246-9eb6-081231ba533b"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Index(['age', 'job', 'marital', 'education', 'default', 'housing', 'loan',\n",
              "       'contact', 'month', 'day_of_week', 'duration', 'campaign', 'pdays',\n",
              "       'previous', 'poutcome', 'emp.var.rate', 'cons.price.idx',\n",
              "       'cons.conf.idx', 'euribor3m', 'nr.employed', 'y'],\n",
              "      dtype='object')"
            ]
          },
          "metadata": {},
          "execution_count": 8
        }
      ],
      "source": [
        "df.columns"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0SDpd1dxKeq4"
      },
      "source": [
        "Input features (column names):\n",
        "\n",
        "1.  `age` - client's age in years (numeric)\n",
        "2.  `job` - type of job (categorical: `admin.`, `blue-collar`, `entrepreneur`, `housemaid`, `management`, `retired`, `self-employed`, `services`, `student`, `technician`, `unemployed`, `unknown`)\n",
        "3.  `marital` - marital status (categorical: `divorced`, `married`, `single`, `unknown`)\n",
        "4.  `education` - client's education (categorical: `basic.4y`, `basic.6y`, `basic.9y`, `high.school`, `illiterate`, `professional.course`, `university.degree`, `unknown`)\n",
        "5.  `default` - has credit in default? (categorical: `no`, `yes`, `unknown`)\n",
        "6.  `housing` - has housing loan? (categorical: `no`, `yes`, `unknown`)\n",
        "7.  `loan` - has personal loan? (categorical: `no`, `yes`, `unknown`)\n",
        "8.  `contact` - contact communication type (categorical: `cellular`, `telephone`)\n",
        "9.  `month` - last contact month of the year (categorical: `jan`, `feb`, `mar`, ..., `nov`, `dec`)\n",
        "10. `day_of_week` - last contact day of the week (categorical: `mon`, `tue`, `wed`, `thu`, `fri`)\n",
        "11. `duration` - last contact duration, in seconds (numeric).\n",
        "12. `campaign` - number of contacts performed and for this client during this campaign (numeric, includes the last contact)\n",
        "13. `pdays` - number of days that have passed after the client was last contacted from the previous campaign (numeric; 999 means the client has not been previously contacted)\n",
        "14. `previous` - number of contacts performed for this client before this campaign (numeric)\n",
        "15. `poutcome` - outcome of the previous marketing campaign (categorical: `failure`, `nonexistent`, `success`)\n",
        "16. `emp.var.rate` - employment variation rate, quarterly indicator (numeric)\n",
        "17. `cons.price.idx` - consumer price index, monthly indicator (numeric)\n",
        "18. `cons.conf.idx` - consumer confidence index, monthly indicator (numeric)\n",
        "19. `euribor3m` - euribor 3 month rate, daily indicator (numeric)\n",
        "20. `nr.employed` - number of employees, quarterly indicator (numeric)\n",
        "\n",
        "Output feature (desired target):\n",
        "\n",
        "21. `y` - has the client subscribed a term deposit? (binary: `yes`,`no`)\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "x6SaYJgj13Z6"
      },
      "source": [
        "To see the general information on all the DataFrame features (columns), we use the **`info`** method:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "LCV1-dAJ13Z6",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "58babb7c-9788-4027-99ba-d5070a257e56"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 41188 entries, 0 to 41187\n",
            "Data columns (total 21 columns):\n",
            " #   Column          Non-Null Count  Dtype  \n",
            "---  ------          --------------  -----  \n",
            " 0   age             41188 non-null  int64  \n",
            " 1   job             41188 non-null  object \n",
            " 2   marital         41188 non-null  object \n",
            " 3   education       41188 non-null  object \n",
            " 4   default         41188 non-null  object \n",
            " 5   housing         41188 non-null  object \n",
            " 6   loan            41188 non-null  object \n",
            " 7   contact         41188 non-null  object \n",
            " 8   month           41188 non-null  object \n",
            " 9   day_of_week     41188 non-null  object \n",
            " 10  duration        41188 non-null  int64  \n",
            " 11  campaign        41188 non-null  int64  \n",
            " 12  pdays           41188 non-null  int64  \n",
            " 13  previous        41188 non-null  int64  \n",
            " 14  poutcome        41188 non-null  object \n",
            " 15  emp.var.rate    41188 non-null  float64\n",
            " 16  cons.price.idx  41188 non-null  float64\n",
            " 17  cons.conf.idx   41188 non-null  float64\n",
            " 18  euribor3m       41188 non-null  float64\n",
            " 19  nr.employed     41188 non-null  float64\n",
            " 20  y               41188 non-null  object \n",
            "dtypes: float64(5), int64(5), object(11)\n",
            "memory usage: 6.6+ MB\n",
            "None\n"
          ]
        }
      ],
      "source": [
        "print(df.info())"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Ic2B0eP0PshN"
      },
      "source": [
        "As we can see, the dataset is full, no pass (`non-null`), so there is no need to fill the gaps. The dataset contains 5 integer (`int64`), 5 real (`float64`) and 11 categorical and binary (`object`) features.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Z2I_fcSH13Z8"
      },
      "source": [
        "Method **`describe`** shows the main statistical characteristics of the dataset for each numerical feature (`int64` and `float64` types): the existing values number, mean, standard deviation, range, min & max, 0.25, 0.5 and 0.75 quartiles.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "id": "JGuHLQMl13Z8",
        "outputId": "95f1f0ce-b2e5-4fa5-aee7-eb1b6f2a7a88"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "           age  duration  campaign    pdays  previous  emp.var.rate  \\\n",
              "count 41188.00  41188.00  41188.00 41188.00  41188.00      41188.00   \n",
              "mean     40.02    258.29      2.57   962.48      0.17          0.08   \n",
              "std      10.42    259.28      2.77   186.91      0.49          1.57   \n",
              "min      17.00      0.00      1.00     0.00      0.00         -3.40   \n",
              "25%      32.00    102.00      1.00   999.00      0.00         -1.80   \n",
              "50%      38.00    180.00      2.00   999.00      0.00          1.10   \n",
              "75%      47.00    319.00      3.00   999.00      0.00          1.40   \n",
              "max      98.00   4918.00     56.00   999.00      7.00          1.40   \n",
              "\n",
              "       cons.price.idx  cons.conf.idx  euribor3m  nr.employed  \n",
              "count        41188.00       41188.00   41188.00     41188.00  \n",
              "mean            93.58         -40.50       3.62      5167.04  \n",
              "std              0.58           4.63       1.73        72.25  \n",
              "min             92.20         -50.80       0.63      4963.60  \n",
              "25%             93.08         -42.70       1.34      5099.10  \n",
              "50%             93.75         -41.80       4.86      5191.00  \n",
              "75%             93.99         -36.40       4.96      5228.10  \n",
              "max             94.77         -26.90       5.04      5228.10  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-60f6d4c8-3730-4315-acfe-29e1c2736f90\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>duration</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "      <td>41188.00</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>40.02</td>\n",
              "      <td>258.29</td>\n",
              "      <td>2.57</td>\n",
              "      <td>962.48</td>\n",
              "      <td>0.17</td>\n",
              "      <td>0.08</td>\n",
              "      <td>93.58</td>\n",
              "      <td>-40.50</td>\n",
              "      <td>3.62</td>\n",
              "      <td>5167.04</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>10.42</td>\n",
              "      <td>259.28</td>\n",
              "      <td>2.77</td>\n",
              "      <td>186.91</td>\n",
              "      <td>0.49</td>\n",
              "      <td>1.57</td>\n",
              "      <td>0.58</td>\n",
              "      <td>4.63</td>\n",
              "      <td>1.73</td>\n",
              "      <td>72.25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>17.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>1.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>-3.40</td>\n",
              "      <td>92.20</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>0.63</td>\n",
              "      <td>4963.60</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>32.00</td>\n",
              "      <td>102.00</td>\n",
              "      <td>1.00</td>\n",
              "      <td>999.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>-1.80</td>\n",
              "      <td>93.08</td>\n",
              "      <td>-42.70</td>\n",
              "      <td>1.34</td>\n",
              "      <td>5099.10</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>38.00</td>\n",
              "      <td>180.00</td>\n",
              "      <td>2.00</td>\n",
              "      <td>999.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.75</td>\n",
              "      <td>-41.80</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>47.00</td>\n",
              "      <td>319.00</td>\n",
              "      <td>3.00</td>\n",
              "      <td>999.00</td>\n",
              "      <td>0.00</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>98.00</td>\n",
              "      <td>4918.00</td>\n",
              "      <td>56.00</td>\n",
              "      <td>999.00</td>\n",
              "      <td>7.00</td>\n",
              "      <td>1.40</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-26.90</td>\n",
              "      <td>5.04</td>\n",
              "      <td>5228.10</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-60f6d4c8-3730-4315-acfe-29e1c2736f90')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-60f6d4c8-3730-4315-acfe-29e1c2736f90 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-60f6d4c8-3730-4315-acfe-29e1c2736f90');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 10
        }
      ],
      "source": [
        "df.describe()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "sJO4lJj113Z9"
      },
      "source": [
        "To see the statistics on non-numeric features, we need to explicitly specify the feature types by the `include` parameter. We can also set `include = all` to output statistics on all the existing features.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "MtLmlp9k13Z-",
        "scrolled": true,
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 175
        },
        "outputId": "1c24fae5-6b78-47a4-a4f0-caf7cb7a62ba"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "           job  marital          education default housing   loan   contact  \\\n",
              "count    41188    41188              41188   41188   41188  41188     41188   \n",
              "unique      12        4                  8       3       3      3         2   \n",
              "top     admin.  married  university.degree      no     yes     no  cellular   \n",
              "freq     10422    24928              12168   32588   21576  33950     26144   \n",
              "\n",
              "        month day_of_week     poutcome      y  \n",
              "count   41188       41188        41188  41188  \n",
              "unique     10           5            3      2  \n",
              "top       may         thu  nonexistent     no  \n",
              "freq    13769        8623        35563  36548  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-badbbfbb-2d81-4a4a-af8d-c9e8fa2555a7\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "      <td>41188</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>unique</th>\n",
              "      <td>12</td>\n",
              "      <td>4</td>\n",
              "      <td>8</td>\n",
              "      <td>3</td>\n",
              "      <td>3</td>\n",
              "      <td>3</td>\n",
              "      <td>2</td>\n",
              "      <td>10</td>\n",
              "      <td>5</td>\n",
              "      <td>3</td>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>top</th>\n",
              "      <td>admin.</td>\n",
              "      <td>married</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>may</td>\n",
              "      <td>thu</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>freq</th>\n",
              "      <td>10422</td>\n",
              "      <td>24928</td>\n",
              "      <td>12168</td>\n",
              "      <td>32588</td>\n",
              "      <td>21576</td>\n",
              "      <td>33950</td>\n",
              "      <td>26144</td>\n",
              "      <td>13769</td>\n",
              "      <td>8623</td>\n",
              "      <td>35563</td>\n",
              "      <td>36548</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-badbbfbb-2d81-4a4a-af8d-c9e8fa2555a7')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-badbbfbb-2d81-4a4a-af8d-c9e8fa2555a7 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-badbbfbb-2d81-4a4a-af8d-c9e8fa2555a7');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 11
        }
      ],
      "source": [
        "df.describe(include = [\"object\"])"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "cMel_T0IRPA5"
      },
      "source": [
        "The result shows that the average client refers to administrative staff (`job = admin.`), is married (`marital = married`) and has a university degree (`education = university.degree`).\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "l0-sAGXl13Z_"
      },
      "source": [
        "For categorical (type `object`) and boolean (type `bool`) features you can use the **`value_counts`** method. Let's look at the target feature (`y`) distribution:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "pjchGbdx13aA",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "6135ba3c-2fa1-4ab1-faa0-cce7df04e611"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "no     36548\n",
              "yes     4640\n",
              "Name: y, dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 12
        }
      ],
      "source": [
        "df[\"y\"].value_counts()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "8P92yMFY13aB"
      },
      "source": [
        "4640 clients (11.3%) of 41188 issued a term deposit, the value of the variable `y` equals `yes`.\n",
        "\n",
        "Let's look at the client distribution by the variable `marital`. Specify the value of the `normalize = True` parameter to view relative frequencies, but not absolute."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "yPqBQPAj13aC",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "42f9d2af-e7b3-4904-a5e9-136e1527a7d4"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "married    0.61\n",
              "single     0.28\n",
              "divorced   0.11\n",
              "unknown    0.00\n",
              "Name: marital, dtype: float64"
            ]
          },
          "metadata": {},
          "execution_count": 13
        }
      ],
      "source": [
        "df[\"marital\"].value_counts(normalize = True)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "DjpEnpfUTaKa"
      },
      "source": [
        "As we can see, 61% (0.61) of clients are married, which must be taken into account when planning marketing campaigns to manage deposit operations.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "IuChKGTT13aC"
      },
      "source": [
        "### Sorting\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "hVb-TBY486e0"
      },
      "source": [
        "A `DataFrame` can be sorted by a few feature values. In our case, for example, by `duration` (`ascending = False` for sorting in descending order):\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "2cPhMArw13aD",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "outputId": "c5759d67-f38b-4dc9-b7e8-fd08c5a1c6f8"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       age          job  marital            education default housing loan  \\\n",
              "24091   33   technician   single  professional.course      no     yes   no   \n",
              "22192   52  blue-collar  married             basic.4y      no      no   no   \n",
              "40537   27       admin.   single          high.school      no      no   no   \n",
              "13820   31   technician  married  professional.course      no      no   no   \n",
              "7727    37   unemployed  married  professional.course      no     yes   no   \n",
              "\n",
              "         contact month day_of_week  ...  campaign  pdays  previous  \\\n",
              "24091  telephone   nov         mon  ...         1    999         0   \n",
              "22192  telephone   aug         thu  ...         3    999         0   \n",
              "40537  telephone   aug         fri  ...         1    999         0   \n",
              "13820   cellular   jul         thu  ...         1    999         0   \n",
              "7727   telephone   may         fri  ...         2    999         0   \n",
              "\n",
              "          poutcome emp.var.rate  cons.price.idx  cons.conf.idx  euribor3m  \\\n",
              "24091  nonexistent        -0.10           93.20         -42.00       4.41   \n",
              "22192  nonexistent         1.40           93.44         -36.10       4.96   \n",
              "40537  nonexistent        -1.70           94.03         -38.30       0.89   \n",
              "13820  nonexistent         1.40           93.92         -42.70       4.96   \n",
              "7727   nonexistent         1.10           93.99         -36.40       4.86   \n",
              "\n",
              "       nr.employed    y  \n",
              "24091      5195.80   no  \n",
              "22192      5228.10  yes  \n",
              "40537      4991.60   no  \n",
              "13820      5228.10  yes  \n",
              "7727       5191.00  yes  \n",
              "\n",
              "[5 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-835fdea8-1186-4a8f-9063-32956ed57dee\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>24091</th>\n",
              "      <td>33</td>\n",
              "      <td>technician</td>\n",
              "      <td>single</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>nov</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-0.10</td>\n",
              "      <td>93.20</td>\n",
              "      <td>-42.00</td>\n",
              "      <td>4.41</td>\n",
              "      <td>5195.80</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>22192</th>\n",
              "      <td>52</td>\n",
              "      <td>blue-collar</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.4y</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>aug</td>\n",
              "      <td>thu</td>\n",
              "      <td>...</td>\n",
              "      <td>3</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.44</td>\n",
              "      <td>-36.10</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>40537</th>\n",
              "      <td>27</td>\n",
              "      <td>admin.</td>\n",
              "      <td>single</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>aug</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>-1.70</td>\n",
              "      <td>94.03</td>\n",
              "      <td>-38.30</td>\n",
              "      <td>0.89</td>\n",
              "      <td>4991.60</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>13820</th>\n",
              "      <td>31</td>\n",
              "      <td>technician</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>jul</td>\n",
              "      <td>thu</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.92</td>\n",
              "      <td>-42.70</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7727</th>\n",
              "      <td>37</td>\n",
              "      <td>unemployed</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>2</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-835fdea8-1186-4a8f-9063-32956ed57dee')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-835fdea8-1186-4a8f-9063-32956ed57dee button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-835fdea8-1186-4a8f-9063-32956ed57dee');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 14
        }
      ],
      "source": [
        "df.sort_values(by = \"duration\", ascending = False).head()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0FBBnPZ1Uiy5"
      },
      "source": [
        "The sorting results show that the longest calls exceed one hour, as the value `duration` is more than 3600 seconds or 1 hour. At the same time, it usually was on Mondays and Thursdays (`day_of_week`) and, especially, in November and August (`month`).\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "OGVjGnbg13aE"
      },
      "source": [
        "Sort by the column group:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "AqfjeNAS13aE",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "outputId": "17e23631-540e-44f9-e7b9-fdcb42f37c60"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       age      job marital education default  housing     loan   contact  \\\n",
              "38274   17  student  single   unknown      no       no      yes  cellular   \n",
              "37579   17  student  single  basic.9y      no  unknown  unknown  cellular   \n",
              "37140   17  student  single   unknown      no      yes       no  cellular   \n",
              "37539   17  student  single  basic.9y      no      yes       no  cellular   \n",
              "37558   17  student  single  basic.9y      no      yes       no  cellular   \n",
              "\n",
              "      month day_of_week  ...  campaign  pdays  previous  poutcome  \\\n",
              "38274   oct         tue  ...         1      2         2   success   \n",
              "37579   aug         fri  ...         2    999         1   failure   \n",
              "37140   aug         wed  ...         3      4         2   success   \n",
              "37539   aug         fri  ...         2    999         2   failure   \n",
              "37558   aug         fri  ...         3      4         2   success   \n",
              "\n",
              "      emp.var.rate  cons.price.idx  cons.conf.idx  euribor3m  nr.employed    y  \n",
              "38274        -3.40           92.43         -26.90       0.74      5017.50  yes  \n",
              "37579        -2.90           92.20         -31.40       0.87      5076.20  yes  \n",
              "37140        -2.90           92.20         -31.40       0.88      5076.20   no  \n",
              "37539        -2.90           92.20         -31.40       0.87      5076.20   no  \n",
              "37558        -2.90           92.20         -31.40       0.87      5076.20   no  \n",
              "\n",
              "[5 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-7a4d2ef3-9d81-41bf-9ad3-349dbfd2a70f\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>38274</th>\n",
              "      <td>17</td>\n",
              "      <td>student</td>\n",
              "      <td>single</td>\n",
              "      <td>unknown</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>cellular</td>\n",
              "      <td>oct</td>\n",
              "      <td>tue</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>2</td>\n",
              "      <td>2</td>\n",
              "      <td>success</td>\n",
              "      <td>-3.40</td>\n",
              "      <td>92.43</td>\n",
              "      <td>-26.90</td>\n",
              "      <td>0.74</td>\n",
              "      <td>5017.50</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>37579</th>\n",
              "      <td>17</td>\n",
              "      <td>student</td>\n",
              "      <td>single</td>\n",
              "      <td>basic.9y</td>\n",
              "      <td>no</td>\n",
              "      <td>unknown</td>\n",
              "      <td>unknown</td>\n",
              "      <td>cellular</td>\n",
              "      <td>aug</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>2</td>\n",
              "      <td>999</td>\n",
              "      <td>1</td>\n",
              "      <td>failure</td>\n",
              "      <td>-2.90</td>\n",
              "      <td>92.20</td>\n",
              "      <td>-31.40</td>\n",
              "      <td>0.87</td>\n",
              "      <td>5076.20</td>\n",
              "      <td>yes</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>37140</th>\n",
              "      <td>17</td>\n",
              "      <td>student</td>\n",
              "      <td>single</td>\n",
              "      <td>unknown</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>aug</td>\n",
              "      <td>wed</td>\n",
              "      <td>...</td>\n",
              "      <td>3</td>\n",
              "      <td>4</td>\n",
              "      <td>2</td>\n",
              "      <td>success</td>\n",
              "      <td>-2.90</td>\n",
              "      <td>92.20</td>\n",
              "      <td>-31.40</td>\n",
              "      <td>0.88</td>\n",
              "      <td>5076.20</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>37539</th>\n",
              "      <td>17</td>\n",
              "      <td>student</td>\n",
              "      <td>single</td>\n",
              "      <td>basic.9y</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>aug</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>2</td>\n",
              "      <td>999</td>\n",
              "      <td>2</td>\n",
              "      <td>failure</td>\n",
              "      <td>-2.90</td>\n",
              "      <td>92.20</td>\n",
              "      <td>-31.40</td>\n",
              "      <td>0.87</td>\n",
              "      <td>5076.20</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>37558</th>\n",
              "      <td>17</td>\n",
              "      <td>student</td>\n",
              "      <td>single</td>\n",
              "      <td>basic.9y</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>aug</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>3</td>\n",
              "      <td>4</td>\n",
              "      <td>2</td>\n",
              "      <td>success</td>\n",
              "      <td>-2.90</td>\n",
              "      <td>92.20</td>\n",
              "      <td>-31.40</td>\n",
              "      <td>0.87</td>\n",
              "      <td>5076.20</td>\n",
              "      <td>no</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-7a4d2ef3-9d81-41bf-9ad3-349dbfd2a70f')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-7a4d2ef3-9d81-41bf-9ad3-349dbfd2a70f button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-7a4d2ef3-9d81-41bf-9ad3-349dbfd2a70f');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 15
        }
      ],
      "source": [
        "df.sort_values(by = [\"age\", \"duration\"], ascending = [True, False]).head()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "FcV8UApXW0ud"
      },
      "source": [
        "We see that the youngest customers are at the `age` of 17, and the call `duration` exceeded 3 minutes only for three clients, which indicates the ineffectiveness of long-term interaction with such clients.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "YHsAC2Vr13aO"
      },
      "source": [
        "### Application of functions: `apply`, `map` etc.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "UhFtQbGX13aP"
      },
      "source": [
        "**Apply the function to each column:**\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "f9tABUDp13aQ",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "6fec4b19-5ac8-4533-a3ec-0f3262e25036"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "age                      98\n",
              "job                 unknown\n",
              "marital             unknown\n",
              "education           unknown\n",
              "default                 yes\n",
              "housing                 yes\n",
              "loan                    yes\n",
              "contact           telephone\n",
              "month                   sep\n",
              "day_of_week             wed\n",
              "duration               4918\n",
              "campaign                 56\n",
              "pdays                   999\n",
              "previous                  7\n",
              "poutcome            success\n",
              "emp.var.rate           1.40\n",
              "cons.price.idx        94.77\n",
              "cons.conf.idx        -26.90\n",
              "euribor3m              5.04\n",
              "nr.employed         5228.10\n",
              "y                       yes\n",
              "dtype: object"
            ]
          },
          "metadata": {},
          "execution_count": 16
        }
      ],
      "source": [
        "df.apply(np.max)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "2BqG93kcXW57"
      },
      "source": [
        "The oldest client is 98 years old (`age` = 98), and the number of contacts with one of the customers reached 56 (`campaign` = 56).\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "RmAMfWTG13aS"
      },
      "source": [
        "**Apply the function to each column cell**\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ze8tUYHP13aT"
      },
      "source": [
        "The `map` can also be used for **the values replacement in a column** by passing it as an argument dictionary in form of ` {old_value: new_value}  `."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "DchqdQ0_13aU",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        },
        "outputId": "6a9ebcb6-d361-4e32-ba73-62f16c91d4a2"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   age        job  marital    education  default housing loan    contact  \\\n",
              "0   56  housemaid  married     basic.4y       no      no   no  telephone   \n",
              "1   57   services  married  high.school  unknown      no   no  telephone   \n",
              "2   37   services  married  high.school       no     yes   no  telephone   \n",
              "3   40     admin.  married     basic.6y       no      no   no  telephone   \n",
              "4   56   services  married  high.school       no      no  yes  telephone   \n",
              "\n",
              "  month day_of_week  ...  campaign  pdays  previous     poutcome emp.var.rate  \\\n",
              "0   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "1   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "2   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "3   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "4   may         mon  ...         1    999         0  nonexistent         1.10   \n",
              "\n",
              "   cons.price.idx  cons.conf.idx  euribor3m  nr.employed  y  \n",
              "0           93.99         -36.40       4.86      5191.00  0  \n",
              "1           93.99         -36.40       4.86      5191.00  0  \n",
              "2           93.99         -36.40       4.86      5191.00  0  \n",
              "3           93.99         -36.40       4.86      5191.00  0  \n",
              "4           93.99         -36.40       4.86      5191.00  0  \n",
              "\n",
              "[5 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-1137d4e6-0f3f-4128-89ba-98eccbab9332\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>56</td>\n",
              "      <td>housemaid</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.4y</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>57</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>unknown</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>37</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>40</td>\n",
              "      <td>admin.</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.6y</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>56</td>\n",
              "      <td>services</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>1</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>5 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-1137d4e6-0f3f-4128-89ba-98eccbab9332')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-1137d4e6-0f3f-4128-89ba-98eccbab9332 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-1137d4e6-0f3f-4128-89ba-98eccbab9332');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 17
        }
      ],
      "source": [
        "d = {\"no\": 0, \"yes\": 1}\n",
        "df[\"y\"] = df[\"y\"].map(d)\n",
        "df.head()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "1XLFcjst13aE"
      },
      "source": [
        "### Indexing and extracting data\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "5YmO8SzC13aF"
      },
      "source": [
        "A `DataFrame` can be indexed in many ways. In this regard, consider various ways of indexing and extracting data from the DataFrame with simple question examples.\n",
        "\n",
        "We can use the code `dataframe ['name']` to extract a separate column. We use this to answer the question: **What is the share of clients attracted in our DataFrame?**\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "f8G8Ce_I13aF",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "2a1e312a-b0a8-4b5a-c1cd-b1cfd28a0f90"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Share of attracted clients = 11.3%\n"
          ]
        }
      ],
      "source": [
        "print(\"Share of attracted clients =\", '{:.1%}'.format(df[\"y\"].mean()))"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "frbJ1GQp13aG"
      },
      "source": [
        "11,3% is a rather bad indicator for a bank, with such a percentage of attracted customers a business can collapse.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "cauScC7f13aG"
      },
      "source": [
        "Logical indexation by one column of a `DataFrame` is very convenient. It looks like this: `df [p(df['Name']]`, where`  p ` is a certain logical condition that is checked for each element of the `Name` column. The result of such an indexation is a `DataFrame` consisting only of the rows satisfying the condition `p` by the `Name` column.\n",
        "\n",
        "We use this to answer the question: **What are the mean values of numerical features among the attracted clients?**"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "TXXcd0mH13aH",
        "scrolled": true,
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "35c34a5f-d953-42d5-ec9b-a4e4e2d6180d"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "age                40.91\n",
              "duration          553.19\n",
              "campaign            2.05\n",
              "pdays             792.04\n",
              "previous            0.49\n",
              "emp.var.rate       -1.23\n",
              "cons.price.idx     93.35\n",
              "cons.conf.idx     -39.79\n",
              "euribor3m           2.12\n",
              "nr.employed      5095.12\n",
              "y                   1.00\n",
              "dtype: float64"
            ]
          },
          "metadata": {},
          "execution_count": 19
        }
      ],
      "source": [
        "df[df[\"y\"] == 1].mean() "
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "hqYEmztJY-Vf"
      },
      "source": [
        "Thus, the average age of the attracted clients is about 40 (`age` = 40.91), and 2 calls were required to attract them (`campaign` = 2.05).\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ModvYJAq13aH"
      },
      "source": [
        "Combining two previous types of indexation, we will answer the question: **What is the average call duration for the attracted clients**?\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "Ubf3zpbk13aH",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "9b488e88-196d-41de-ce19-e3beca7a016f"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Average call duration for attracted clients = 9.0 min 13 sec\n"
          ]
        }
      ],
      "source": [
        "acd = round(df[df[\"y\"] == 1][\"duration\"].mean(), 2)\n",
        "acd_in_min = acd // 60\n",
        "print(\"Average call duration for attracted clients =\", acd_in_min, \"min\", int(acd) % 60, \"sec\")"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "C9a34m70ZgRa"
      },
      "source": [
        "So, the average duration of a successful call is almost 553 seconds, that is, nearly 10 minutes.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "95VAbA6Z13aJ"
      },
      "source": [
        "**What is the average age of attracted (`y == 1`) and unmarried (`'marital' == 'single'`) clients?**\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "q9Mx-i4r13aK",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "8e20c458-5cfe-4e85-fa98-e9ba8a21eee8"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Average age of attracted clients = 31 years\n"
          ]
        }
      ],
      "source": [
        "print(\"Average age of attracted clients =\", int(df[(df[\"y\"] == 1) & (df[\"marital\"] == \"single\")][\"age\"].mean()), \"years\")"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "5yLFwNHbZ5tm"
      },
      "source": [
        "The average age of unmarried attracted clients is 31, which should be considered when working with such clients.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "5-pVIUlf13aN"
      },
      "source": [
        "If we need to get the first or last line of the DataFrame, we can use the code `df[:1]` or `df[-1:]`:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "Q6uHjTaG13aN",
        "scrolled": true,
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 174
        },
        "outputId": "729a6ff3-cd6f-48bf-870d-041f3a4596f7"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       age      job  marital            education default housing loan  \\\n",
              "41187   74  retired  married  professional.course      no     yes   no   \n",
              "\n",
              "        contact month day_of_week  ...  campaign  pdays  previous  poutcome  \\\n",
              "41187  cellular   nov         fri  ...         3    999         1   failure   \n",
              "\n",
              "      emp.var.rate  cons.price.idx  cons.conf.idx  euribor3m  nr.employed  y  \n",
              "41187        -1.10           94.77         -50.80       1.03      4963.60  0  \n",
              "\n",
              "[1 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-92fb645d-3a12-4721-82c5-6122ca35abbf\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>41187</th>\n",
              "      <td>74</td>\n",
              "      <td>retired</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>nov</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>3</td>\n",
              "      <td>999</td>\n",
              "      <td>1</td>\n",
              "      <td>failure</td>\n",
              "      <td>-1.10</td>\n",
              "      <td>94.77</td>\n",
              "      <td>-50.80</td>\n",
              "      <td>1.03</td>\n",
              "      <td>4963.60</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>1 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-92fb645d-3a12-4721-82c5-6122ca35abbf')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-92fb645d-3a12-4721-82c5-6122ca35abbf button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-92fb645d-3a12-4721-82c5-6122ca35abbf');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 22
        }
      ],
      "source": [
        "df[-1:]"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "1nYYsB2W13aY"
      },
      "source": [
        "## Pivot tables\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "AcIkYgoQ13aY"
      },
      "source": [
        "Suppose we want to see how observations in our sample are distributed in the context of two features - `y` and `marital`. To do this, we can build **cross tabulation** by the `crosstab` method."
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "Xs4C3jZ213aa",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 143
        },
        "outputId": "6b0b9504-af36-43c8-85fa-ee7bde0c8213"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "marital  divorced  married  single  unknown\n",
              "y                                          \n",
              "0            4136    22396    9948       68\n",
              "1             476     2532    1620       12"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-ef290b2b-1d06-480e-b6da-11e2c3a5d923\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>marital</th>\n",
              "      <th>divorced</th>\n",
              "      <th>married</th>\n",
              "      <th>single</th>\n",
              "      <th>unknown</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>y</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>4136</td>\n",
              "      <td>22396</td>\n",
              "      <td>9948</td>\n",
              "      <td>68</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>476</td>\n",
              "      <td>2532</td>\n",
              "      <td>1620</td>\n",
              "      <td>12</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-ef290b2b-1d06-480e-b6da-11e2c3a5d923')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-ef290b2b-1d06-480e-b6da-11e2c3a5d923 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-ef290b2b-1d06-480e-b6da-11e2c3a5d923');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 23
        }
      ],
      "source": [
        "pd.crosstab(df[\"y\"], df[\"marital\"])"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "cS4ybt3rai_A"
      },
      "source": [
        "The result shows that the number of attracted married clients is 2532 (`y = 1` for `married`) from the total number.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "4sVTC0mR13aa",
        "scrolled": true,
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 143
        },
        "outputId": "ed5d0e49-f127-4348-e362-f004b58f6e4b"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "marital  divorced  married  single  unknown\n",
              "y                                          \n",
              "0            0.11     0.61    0.27     0.00\n",
              "1            0.10     0.55    0.35     0.00"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-b13ccaef-adbc-4922-9ec2-3310e9e18620\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>marital</th>\n",
              "      <th>divorced</th>\n",
              "      <th>married</th>\n",
              "      <th>single</th>\n",
              "      <th>unknown</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>y</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>0.11</td>\n",
              "      <td>0.61</td>\n",
              "      <td>0.27</td>\n",
              "      <td>0.00</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>0.10</td>\n",
              "      <td>0.55</td>\n",
              "      <td>0.35</td>\n",
              "      <td>0.00</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-b13ccaef-adbc-4922-9ec2-3310e9e18620')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-b13ccaef-adbc-4922-9ec2-3310e9e18620 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-b13ccaef-adbc-4922-9ec2-3310e9e18620');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 24
        }
      ],
      "source": [
        "pd.crosstab(df[\"y\"],\n",
        "            df[\"marital\"],\n",
        "            normalize = 'index')"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "MONsLf1z13ab"
      },
      "source": [
        "We see that more than half of the clients (61%, column `married`) are married and have not issued a deposit.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "66M5GLW613ab"
      },
      "source": [
        "In `Pandas`, **pivot tables** are implemented by the method `pivot_table` with such parameters:\n",
        "\n",
        "*   `values` – a list of variables to calculate the necessary statistics,\n",
        "*   `index` – a list of variables to group data,\n",
        "*   `aggfunc` — values that we actually need to count by groups - the amount, average, maximum, minimum or something else.\n",
        "\n",
        "Let's find the average age and the call duration for different types of client employment `job`:\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "ebAVIoDt13ac",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 394
        },
        "outputId": "5c650b69-765c-416d-8681-eb24802f4498"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "                age  duration\n",
              "job                          \n",
              "admin.        38.19    254.31\n",
              "blue-collar   39.56    264.54\n",
              "entrepreneur  41.72    263.27\n",
              "housemaid     45.50    250.45\n",
              "management    42.36    257.06\n",
              "retired       62.03    273.71\n",
              "self-employed 39.95    264.14\n",
              "services      37.93    258.40\n",
              "student       25.89    283.68\n",
              "technician    38.51    250.23"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-276e380d-931a-4e27-9d25-7c66f4751f6e\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>duration</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>job</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>admin.</th>\n",
              "      <td>38.19</td>\n",
              "      <td>254.31</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>blue-collar</th>\n",
              "      <td>39.56</td>\n",
              "      <td>264.54</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>entrepreneur</th>\n",
              "      <td>41.72</td>\n",
              "      <td>263.27</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>housemaid</th>\n",
              "      <td>45.50</td>\n",
              "      <td>250.45</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>management</th>\n",
              "      <td>42.36</td>\n",
              "      <td>257.06</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>retired</th>\n",
              "      <td>62.03</td>\n",
              "      <td>273.71</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>self-employed</th>\n",
              "      <td>39.95</td>\n",
              "      <td>264.14</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>services</th>\n",
              "      <td>37.93</td>\n",
              "      <td>258.40</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>student</th>\n",
              "      <td>25.89</td>\n",
              "      <td>283.68</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>technician</th>\n",
              "      <td>38.51</td>\n",
              "      <td>250.23</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-276e380d-931a-4e27-9d25-7c66f4751f6e')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-276e380d-931a-4e27-9d25-7c66f4751f6e button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-276e380d-931a-4e27-9d25-7c66f4751f6e');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 25
        }
      ],
      "source": [
        "df.pivot_table(\n",
        "    [\"age\", \"duration\"],\n",
        "    [\"job\"],\n",
        "    aggfunc = \"mean\",\n",
        ").head(10)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "7gj2inIUb1U7"
      },
      "source": [
        "The obtained results allow us to plan marketing banking campaigns more effectively.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "omZ1hAP1FVIH"
      },
      "source": [
        "## Visualization in Pandas\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "G0sVMyqlFVIH"
      },
      "source": [
        "Method **scatter_matrix** allows you to visualize the pairwise dependencies between the features (as well as the distribution of each feature on the diagonal). We will do it for numerical features.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "_8CueXbuFVII",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 891
        },
        "outputId": "1b244b44-939f-46d7-a4d9-13c500736ac3"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 1080x1080 with 9 Axes>"
            ],
            "image/png": "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yRIpZfhEJLcU8ImIiIjkmdvJZPiSyvCJSG4p4BMRERHJM7emdIrILFHAJyIiIpJn7uyUTgV8IpJbCvhERERE8uzclE6t4ROR3FLAJyIiIpJnmtIpIrMl7wGfMabNGNNljPmxMeaHmes+Y4x53hjzVWOMJ99jFBEREZlN2SmdKtoiIjmW94Av40lr7TZr7b3GmDrgTmvtrcBrwDvyPDYRERGRWTWW4UuqLYOI5FihBHx3GmOeM8b8CrAR+HHm+h8BW/I2KhEREZGrYGwNX1wZPhHJMXe+BwB0AEuBKPAoUAp0Z24LAhV5GpeIiIjIVeFyxjJ8CvhEJLfynuGz1kattSPW2gTwPeAoUJa5uQwYvPAxxpiPGmN2GGN29PT0XMXRioiIiOSex5X+ShbXlE4RybG8B3zGmNJxF28BjgB3ZC7fDbx04WOstV+01m601m6sra29CqMUERERmT3ZDJ+mdIpIjuU94ANuM8bsNMa8AJy11r4MPGuMeR5YC3w7v8MTERERmV3ZNXya0ikiOZb3NXzW2seBxy+47k+AP8nPiERERESuLmMMLseoSqeI5FwhZPhERERErntux6jxuojknAI+ERERkQLgdowar4tIzingExERESkAbpejtgwiknMK+EREREQKgNsxxJNawyciuaWAT0RERKQAuF1GGT4RyTkFfCIiIiIFwO04xLWGT0RyTAGfiIiISAFIZ/g0pVNEcksBn4iIiEgBcDlGjddFJOcU8ImIiIgUAI/jkNSUThHJMQV8IiIiIgXA5RgSmtIpIjmmgE9ERESkAHhchoSmdIpIjingExERESkALseQ0JROEckxBXwiIiIiBcDtcjSlU0RyTgGfiIiISAFwK8MnIrNAAZ+IiIhIAXC7HLVlEJGcU8AnIiIiUgDcjiGlgE9EckwBn4iIiEgBSLdlUMAnIrmlgE9ERESkALiMIamiLSKSYwr4RERERAqAS334RGQWKOATERERKQBawycis0EBn4iIiEgB0Bo+EZkNCvhERERECoDbMSQV8IlIjingExERESkALsdRhk9Eck4Bn4iIiEgBUIZPRGaDAj4RERGRAuByDImk2jKISG4p4BMREREpAMrwichsUMAnIiIiUgDUh09EZoM73wOQiUUTSR59tZ3B0RhvXt1IS1Ug30MqKNZantjbycm+MLctqWF1c3m+hyTXidP9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\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "pd.plotting.scatter_matrix(\n",
        "    df[[\"age\", \"duration\", \"campaign\"]],\n",
        "    figsize = (15, 15),\n",
        "    diagonal = \"kde\")\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "i1RN2MBidNJX"
      },
      "source": [
        "A scatter matrix (pairs plot) compactly plots all the numeric variables we have in a dataset against each other.\n",
        "The plots on the main diagonal allow you to visually define the type of data distribution: the distribution is similar to normal for age, and for a call duration and the number of contacts, the [geometric distribution](https://en.wikipedia.org/wiki/geometric_distribution?utm_medium=Exinfluencer\\&utm_source=Exinfluencer\\&utm_content=000026UJ\\&utm_term=10006555\\&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkQuickLabsEDA_Pandas_Banking_L126457256-2021-01-01) is more suitable.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "zEAaz2PIFVII"
      },
      "source": [
        "**Now We will build a separate histogram for `age` feature:**\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "SJOQB60_FVII",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 391
        },
        "outputId": "3c199473-4a39-484c-fdad-9fc915cf48eb"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.axes._subplots.AxesSubplot at 0x7fab3a620890>"
            ]
          },
          "metadata": {},
          "execution_count": 27
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 576x432 with 1 Axes>"
            ],
            "image/png": "iVBORw0KGgoAAAANSUhEUgAAAfMAAAFlCAYAAAD/MAEVAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAaF0lEQVR4nO3dfZBd9X3f8fe3KGBACeLB3SGSWtFBtQejmMAO4HHqWUEKAjyWp2O7UMYID4n+KE5wqhlbNOOS2GYGT00InjikmogaP5SFEKeogI0VzI6bTnmSwQiQCRuQjTQYHAtwZYjrJd/+cX+Ca3WXXe3dh/tdvV8zd/ac3/ndc37fuefu556HvRuZiSRJquufzPcAJElSbwxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKWzTfA5iu4447LlesWDHfwwDgpz/9KUceeeR8D6Nn1tFfrKP/LJRarKO/TLWObdu2/X1mvnW8ZWXDfMWKFTz00EPzPQwARkZGGBoamu9h9Mw6+ot19J+FUot19Jep1hER359omafZJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOImDfOIuDEiXoiIx7ra/nNEfC8iHo2Iv4qIJV3LroyI0Yh4MiLO7Wpf09pGI2JjV/sJEXF/a78lIg6dyQIlSVropnJk/kVgzX5tW4GTM/PXgL8FrgSIiJOAC4F3tOf8aUQcEhGHAF8AzgNOAi5qfQE+C1yXmScCLwKX9VSRJEkHmUn/a1pmfjsiVuzX9s2u2fuAD7TptcBwZv4MeCYiRoHT27LRzHwaICKGgbURsQM4C/h3rc9NwB8AN0ynGM2vFRvvnO8hALBh1RiXTjCWnddcMMejkaTZF5k5eadOmN+RmSePs+x/ALdk5lci4k+A+zLzK23ZZuDrreuazPyt1v5h4Aw6wX1fOyonIpYDXx9vO235emA9wMDAwGnDw8NTr3QW7d27l8WLF8/3MHrWax3bd788g6OZvoHD4flXx1+2aulRczuYHrhf9Z+FUot19Jep1rF69eptmTk43rKe/p95RPw+MAZ8tZf1TFVmbgI2AQwODma//B/bg+1/6k5koqPhubZh1RjXbh9/19558dDcDqYH7lf9Z6HUYh39ZSbqmHaYR8SlwHuBs/ONw/vdwPKubstaGxO0/xhYEhGLMnNsv/6SJGkKpvWnaRGxBvg48L7MfKVr0Rbgwog4LCJOAFYCDwAPAivbneuH0rlJbkv7EHAvb1xzXwfcPr1SJEk6OE3lT9NuBv438LaI2BURlwF/AvwysDUiHomIPwPIzMeBW4EngG8Al2fma+2o+6PA3cAO4NbWF+ATwH9oN8sdC2ye0QolSVrgpnI3+0XjNE8YuJl5NXD1OO13AXeN0/40b9zxLkmSDpDfACdJUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQV19P/M9fcWjHL/y98w6qxvvmf5JKkqfPIXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKmzTMI+LGiHghIh7rajsmIrZGxFPt59GtPSLi8xExGhGPRsSpXc9Z1/o/FRHrutpPi4jt7Tmfj4iY6SIlSVrIpnJk/kVgzX5tG4F7MnMlcE+bBzgPWNke64EboBP+wFXAGcDpwFX7PgC0Pr/d9bz9tyVJkt7EpGGemd8G9uzXvBa4qU3fBLy/q/1L2XEfsCQijgfOBbZm5p7MfBHYCqxpy34lM+/LzAS+1LUuSZI0BdO9Zj6Qmc+16R8CA216KfBsV79dre3N2neN0y5JkqZoUa8ryMyMiJyJwUwmItbTOX3PwMAAIyMjc7HZSe3du3dOxrJh1disrn/g8Nnfxlx4szr6ZZ+Zirnar2bbQqkDFk4t1tFfZqKO6Yb58xFxfGY+106Vv9DadwPLu/ota227gaH92kda+7Jx+o8rMzcBmwAGBwdzaGhooq5zamRkhLkYy6Ub75zV9W9YNca123v+fDfv3qyOnRcPze1gejBX+9VsWyh1wMKpxTr6y0zUMd3T7FuAfXekrwNu72q/pN3VfibwcjsdfzdwTkQc3W58Owe4uy37SUSc2e5iv6RrXZIkaQomPQyLiJvpHFUfFxG76NyVfg1wa0RcBnwf+FDrfhdwPjAKvAJ8BCAz90TEp4EHW79PZea+m+r+PZ075g8Hvt4ekiRpiiYN88y8aIJFZ4/TN4HLJ1jPjcCN47Q/BJw82TgkSdL4/AY4SZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqbiewjwifi8iHo+IxyLi5oh4S0ScEBH3R8RoRNwSEYe2voe1+dG2fEXXeq5s7U9GxLm9lSRJ0sFl0XSfGBFLgd8FTsrMVyPiVuBC4Hzguswcjog/Ay4Dbmg/X8zMEyPiQuCzwL+NiJPa894B/Crw1xHxLzPztZ4qk8axYuOd8z2EN7XzmgvmewiSCur1NPsi4PCIWAQcATwHnAXc1pbfBLy/Ta9t87TlZ0dEtPbhzPxZZj4DjAKn9zguSZIOGpGZ039yxBXA1cCrwDeBK4D7MvPEtnw58PXMPDkiHgPWZOautuzvgDOAP2jP+Upr39yec9s421sPrAcYGBg4bXh4eNpjn0l79+5l8eLFs76d7btfntX1DxwOz786q5uYE5XrWLX0qNen52q/mm0LpQ5YOLVYR3+Zah2rV6/elpmD4y3r5TT70XSOqk8AXgL+Algz3fVNRWZuAjYBDA4O5tDQ0GxubspGRkaYi7FcOsuniDesGuPa7dPeJfpG5Tp2Xjz0+vRc7VezbaHUAQunFuvoLzNRRy+n2X8TeCYzf5SZPwe+BrwbWNJOuwMsA3a36d3AcoC2/Cjgx93t4zxHkiRNopcw/wFwZkQc0a59nw08AdwLfKD1WQfc3qa3tHna8m9l5xz/FuDCdrf7CcBK4IEexiVJ0kFl2uciM/P+iLgN+A4wBjxM5xT4ncBwRHymtW1uT9kMfDkiRoE9dO5gJzMfb3fCP9HWc7l3skuSNHU9XVjMzKuAq/Zrfppx7kbPzH8APjjBeq6mcyOdJEk6QH4DnCRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklScYS5JUnGGuSRJxRnmkiQVZ5hLklRcT2EeEUsi4raI+F5E7IiId0XEMRGxNSKeaj+Pbn0jIj4fEaMR8WhEnNq1nnWt/1MRsa7XoiRJOpj0emR+PfCNzHw78E5gB7ARuCczVwL3tHmA84CV7bEeuAEgIo4BrgLOAE4Hrtr3AUCSJE1u2mEeEUcB7wE2A2Tm/83Ml4C1wE2t203A+9v0WuBL2XEfsCQijgfOBbZm5p7MfBHYCqyZ7rgkSTrYRGZO74kRpwCbgCfoHJVvA64AdmfmktYngBczc0lE3AFck5l/05bdA3wCGALekpmfae2fBF7NzM+Ns831dI7qGRgYOG14eHhaY59pe/fuZfHixbO+ne27X57V9Q8cDs+/OqubmBOV61i19KjXp+dqv5ptC6UOWDi1WEd/mWodq1ev3paZg+MtW9TD9hcBpwK/k5n3R8T1vHFKHYDMzIiY3qeFcWTmJjofIBgcHMyhoaGZWnVPRkZGmIuxXLrxzlld/4ZVY1y7vZddoj9UrmPnxUOvT8/VfjXbFkodsHBqsY7+MhN19HLNfBewKzPvb/O30Qn359vpc9rPF9ry3cDyrucva20TtUuSpCmYdphn5g+BZyPiba3pbDqn3LcA++5IXwfc3qa3AJe0u9rPBF7OzOeAu4FzIuLoduPbOa1NkiRNQa/nIn8H+GpEHAo8DXyEzgeEWyPiMuD7wIda37uA84FR4JXWl8zcExGfBh5s/T6VmXt6HJckSQeNnsI8Mx8BxrsYf/Y4fRO4fIL13Ajc2MtYpIVgRdd9ERtWjc36fRLTsfOaC+Z7CJL24zfASZJUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxPYd5RBwSEQ9HxB1t/oSIuD8iRiPilog4tLUf1uZH2/IVXeu4srU/GRHn9jomSZIOJjNxZH4FsKNr/rPAdZl5IvAicFlrvwx4sbVf1/oREScBFwLvANYAfxoRh8zAuCRJOij0FOYRsQy4APjzNh/AWcBtrctNwPvb9No2T1t+duu/FhjOzJ9l5jPAKHB6L+OSJOlg0uuR+R8DHwf+sc0fC7yUmWNtfhewtE0vBZ4FaMtfbv1fbx/nOZIkaRKLpvvEiHgv8EJmbouIoZkb0ptucz2wHmBgYICRkZG52Oyk9u7dOydj2bBqbPJOPRg4fPa3MResY3Yd6L4+V++PubBQarGO/jITdUw7zIF3A++LiPOBtwC/AlwPLImIRe3oexmwu/XfDSwHdkXEIuAo4Mdd7ft0P+cXZOYmYBPA4OBgDg0N9TD8mTMyMsJcjOXSjXfO6vo3rBrj2u297BL9wTpm186Lhw6o/1y9P+bCQqnFOvrLTNQx7dPsmXllZi7LzBV0bmD7VmZeDNwLfKB1Wwfc3qa3tHna8m9lZrb2C9vd7icAK4EHpjsuSZIONrPxsf8TwHBEfAZ4GNjc2jcDX46IUWAPnQ8AZObjEXEr8AQwBlyema/NwrgkSVqQZiTMM3MEGGnTTzPO3eiZ+Q/AByd4/tXA1TMxFkmSDjZ+A5wkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JUnGEuSVJxhrkkScUZ5pIkFWeYS5JU3LTDPCKWR8S9EfFERDweEVe09mMiYmtEPNV+Ht3aIyI+HxGjEfFoRJzata51rf9TEbGu97IkSTp49HJkPgZsyMyTgDOByyPiJGAjcE9mrgTuafMA5wEr22M9cAN0wh+4CjgDOB24at8HAEmSNLlph3lmPpeZ32nT/wfYASwF1gI3tW43Ae9v02uBL2XHfcCSiDgeOBfYmpl7MvNFYCuwZrrjkiTpYBOZ2ftKIlYA3wZOBn6QmUtaewAvZuaSiLgDuCYz/6Ytuwf4BDAEvCUzP9PaPwm8mpmfG2c76+kc1TMwMHDa8PBwz2OfCXv37mXx4sWzvp3tu1+e1fUPHA7Pvzqrm5gT1jG7Vi096oD6z9X7Yy4slFqso79MtY7Vq1dvy8zB8ZYt6nUQEbEY+EvgY5n5k05+d2RmRkTvnxbeWN8mYBPA4OBgDg0NzdSqezIyMsJcjOXSjXfO6vo3rBrj2u097xLzzjpm186Lhw6o/1y9P+bCQqnFOvrLTNTR093sEfFLdIL8q5n5tdb8fDt9Tvv5QmvfDSzvevqy1jZRuyRJmoJe7mYPYDOwIzP/qGvRFmDfHenrgNu72i9pd7WfCbycmc8BdwPnRMTR7ca3c1qbJEmagl7O4b0b+DCwPSIeaW3/EbgGuDUiLgO+D3yoLbsLOB8YBV4BPgKQmXsi4tPAg63fpzJzTw/jkiTpoDLtMG83ssUEi88ep38Cl0+wrhuBG6c7FkmSDmZ+A5wkScUZ5pIkFWeYS5JUXP/9Ees8WdHD33BvWDU2638DLknSRAxzSQfkQD/4zvWH3Z3XXDBn25L6hafZJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqzjCXJKk4w1ySpOIMc0mSijPMJUkqbtF8D0CSZtKKjXfO2ro3rBrj0hlY/85rLpiB0Uhv8MhckqTiDHNJkorzNLskzbHZvBQwFVO5XOClgFr65sg8ItZExJMRMRoRG+d7PJIkVdEXYR4RhwBfAM4DTgIuioiT5ndUkiTV0C+n2U8HRjPzaYCIGAbWAk/M66gk6SA135cCJuNlgF/UF0fmwFLg2a75Xa1NkiRNIjJzvsdARHwAWJOZv9XmPwyckZkf3a/femB9m30b8OScDnRixwF/P9+DmAHW0V+so/8slFqso79MtY5/nplvHW9Bv5xm3w0s75pf1tp+QWZuAjbN1aCmKiIeyszB+R5Hr6yjv1hH/1kotVhHf5mJOvrlNPuDwMqIOCEiDgUuBLbM85gkSSqhL47MM3MsIj4K3A0cAtyYmY/P87AkSSqhL8IcIDPvAu6a73FMU9+d+p8m6+gv1tF/Fkot1tFfeq6jL26AkyRJ09cv18wlSdI0GeYHICKWR8S9EfFERDweEVe09mMiYmtEPNV+Hj3fY51MRLwlIh6IiO+2Wv6wtZ8QEfe3r9W9pd2Q2Nci4pCIeDgi7mjz5WoAiIidEbE9Ih6JiIdaW8V9a0lE3BYR34uIHRHxrmp1RMTb2uuw7/GTiPhYtToAIuL32nv8sYi4ub33y71HIuKKVsPjEfGx1lbi9YiIGyPihYh4rKtt3LFHx+fba/NoRJw6lW0Y5gdmDNiQmScBZwKXt6+d3Qjck5krgXvafL/7GXBWZr4TOAVYExFnAp8FrsvME4EXgcvmcYxTdQWwo2u+Yg37rM7MU7r+TKXivnU98I3MfDvwTjqvTak6MvPJ9jqcApwGvAL8FcXqiIilwO8Cg5l5Mp0bjC+k2HskIk4GfpvOt4W+E3hvRJxIndfji8Ca/domGvt5wMr2WA/cMKUtZKaPaT6A24F/TefLa45vbccDT8732A6wjiOA7wBn0PnigkWt/V3A3fM9vknGvqy9Ec4C7gCiWg1dtewEjtuvrdS+BRwFPEO7H6dqHfuN/Rzgf1Wsgze+XfMYOjc83wGcW+09AnwQ2Nw1/0ng45VeD2AF8FjX/LhjB/4LcNF4/d7s4ZH5NEXECuDXgfuBgcx8ri36ITAwT8M6IO309CPAC8BW4O+AlzJzrHWp8LW6f0znTf2Pbf5Y6tWwTwLfjIht7dsOod6+dQLwI+C/tksffx4RR1Kvjm4XAje36VJ1ZOZu4HPAD4DngJeBbdR7jzwG/KuIODYijgDOp/NFY6Vej/1MNPZpfb25YT4NEbEY+EvgY5n5k+5l2fkoVeJPBDLzteycRlxG5/TV2+d5SAckIt4LvJCZ2+Z7LDPkNzLzVDqn2S6PiPd0Lyyyby0CTgVuyMxfB37Kfqc+i9QBQLuW/D7gL/ZfVqGOdh12LZ0PWb8KHMn/f7q372XmDjqXBr4JfAN4BHhtvz59/3pMZCbGbpgfoIj4JTpB/tXM/Fprfj4ijm/Lj6dzpFtGZr4E3EvndNuSiNj3/QPjfq1uH3k38L6I2AkM0znVfj21anhdO4oiM1+gc332dOrtW7uAXZl5f5u/jU64V6tjn/OA72Tm822+Wh2/CTyTmT/KzJ8DX6Pzvin3HsnMzZl5Wma+h851/r+l3uvRbaKxT+nrzfdnmB+AiAhgM7AjM/+oa9EWYF2bXkfnWnpfi4i3RsSSNn04nWv/O+iE+gdat76uJTOvzMxlmbmCzqnQb2XmxRSqYZ+IODIifnnfNJ3rtI9RbN/KzB8Cz0bE21rT2XT+lXGpOrpcxBun2KFeHT8AzoyII9rvr32vR8X3yD9tP/8Z8G+A/0a916PbRGPfAlzS7mo/E3i563T8xOb7poBKD+A36JwKeZTOaZ5H6Fy7OZbOTVhPAX8NHDPfY51CLb8GPNxqeQz4T639XwAPAKN0Ti0eNt9jnWI9Q8AdVWtoY/5uezwO/H5rr7hvnQI81Pat/w4cXbSOI4EfA0d1tVWs4w+B77X3+ZeBw4q+R/4nnQ8i3wXOrvR60PlA+Bzwczpnry6baOx0buL9Ap17mLbT+UuESbfhN8BJklScp9klSSrOMJckqTjDXJKk4gxzSZKKM8wlSSrOMJckqTjDXJKk4gxzSZKK+38hFc9r/phoWwAAAABJRU5ErkJggg==\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "df[\"age\"].hist()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "CjnmCPbFefXl"
      },
      "source": [
        "The histogram shows that most of our clients are between the ages of 25 and 50, which corresponds to the actively working part of the population.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "-1A59i55FVIJ"
      },
      "source": [
        "**Now we will build histogram for features all together:**\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "H5oIPZa0FVIJ",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 607
        },
        "outputId": "9440552e-e53d-4a19-d5f8-b7d7cd84629a"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 1080x720 with 12 Axes>"
            ],
            "image/png": "iVBORw0KGgoAAAANSUhEUgAAA3kAAAJOCAYAAAAK+M50AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjIsIGh0dHA6Ly9tYXRwbG90bGliLm9yZy+WH4yJAAAgAElEQVR4nOzde5hlVX3n//dH8IrIRUwHu9HGkcRBJ0HtAI6ZpFsTbppgMsZIjKAhYSbiRGckEZL8gvEyY2YgRifGhCgCRgXiJTIEgwS7xjFPQGg1XCW0CKE7CMrVxqhBv78/9io8FFXVVd2n6uxz6v16nvPU2Wtfznefc+p79tp77bVSVUiSJEmSJsMjRh2AJEmSJGl4rORJkiRJ0gSxkidJkiRJE8RKniRJkiRNECt5kiRJkjRBrORJkiRJ0gSxkidJWhGSnJXkrcv0Wq9I8qnleC1JWipJtiV52qjj0OJZyZMkaSckWZukkuw6XVZVH6yqw0YZlyTtrKp6fFXdNOo4tHhW8iRJmkeSXUYdgyRJi2ElT0sqyclJvpzkG0muS/JzrXyXJKcn+XqSryR57eCZ8CR7JHlfktuSbE3yVg+0JC1Gkmcn+XzLP+cBj2nlr0ry2RnLVpKnt+dnJXlPkouS3A9sSPKiJF9Icl+SW5O8aWD1z7S/97SmTc+b+RpJ/n2SK5Lc2/7++4F5U0nekuTvWqyfSrLPEr0tknokyX5JPpbka0nuTPLHSf5Nkk+36a8n+WCSPQfWuTnJbya5Ksn97XhpVZJPthzyt0n2astOtzQ4Ick/t+Oqkwa2dXCSv09yT5v3x0keNTB/MDc+Mcn/aXnwinZs9tkZy/7nJDe27b07SZbnndRMVvK01L4M/AdgD+D3gb9Isi/wa8CRwEHAc4CXzFjvLOAB4OnAs4HDgF9dnpAljbt2kPJXwAeAvYG/BP7jIjbxS8DbgN2BzwL3A8cCewIvAn49yXTe+on2d8/WtOnvZ8SyN/DXwLuAJwJ/CPx1kifOeL1XAz8APAo4CUkTrZ28vhC4BVgLrAbOBQL8D+DJwL8F9gPeNGP1/wj8NPBDwM8AnwR+G3gS3fH9b8xYfgNwAN3x1BuT/FQr/y7wX4F9gOcBLwReM0fI76bLhT8IHNceM70Y+DHgR4CXAYfPtf9aWlbytKSq6i+r6p+r6ntVdR5wI3Aw3T/+O6tqS1XdDbx9ep0kq4CjgNdX1f1VdQfwDuDlI9gFSePpUOCRwB9V1b9W1UeAKxax/ieq6u9a7vpWVU1V1dVt+irgw8BPLnBbLwJurKoPVNUDVfVh4Et0B2bT3l9V/1hV/wKcT3cCTNJkO5iuIveb7XjnW1X12araXFWXVNW3q+prdCeGZuab/11Vt1fVVuD/AZdX1Req6lvAx+lOkA/6/fYaVwPvB44BqKpNVXVZy003A382y2tNV0j/I3BqVX2zqq4Dzp5ln95eVfdU1T8BGzGXjcyu219E2nFJjgX+G90ZKoDH050tejJw68Cig8+fSndwdtvAVf5HzFhGkubzZGBrVdVA2S2LWP8h+SbJIXQno55Fd6Xt0XRXBxcay8zXvoXurP20rw48/yZdrpQ02fYDbqmqBwYL28nud9K1hNqd7hjo7hnr3j7w/F9mmZ6ZQwZz2i3Av2uv9UN0lch1wOPo6gabZon1SW3eXMdu08xlPeGVPC2ZJE8F/hx4LfDEqtoTuIauGcJtwJqBxfcbeH4r8G1gn6rasz2eUFXPXKbQJY2/24DVM+4HeUr7ez/dwQwASX5wlvVrxvSHgAuA/apqD+BP6XLZbMvO9M90J68GPQXYup31JE22W4GnDPbM2/x3urzy76rqCcAv8/18s6MGj7OeQpeXAN5D17LggPZavz3Ha32N7jaauY7d1DNW8rSUdqNLUl8DSPJqurPg0DVHel2S1e1m4jdOr1RVtwGfAk5P8oQkj2g3IS+0aZQk/T3dAclvJHlkkp+naxoF8A/AM5MclOQxPPxel9nsDtxVVd9KcjDdPXTTvgZ8D5hrLKmLgB9K8ktJdk3yi8CBdPfiSFq5Pkd3QurtSXZL8pgkz6fLN9uAe5OsBn5zCK/1/yV5XJJn0t3/e14r3x24D9iW5BnAr8+2clV9F/gY8Ka2nWfQ3aesnrKSpyXT2mufTnewdTtd04C/a7P/nK4idxXwBbqDoAfobgCGLnE8CriOronCR4B9lyt2SeOtqr4D/DzwKuAu4BfpDlCoqn8E3gz8Ld19wp+dfSsP8RrgzUm+Afwe3Ymq6df6Jl0nLX/XepQ7dEYsd9J1RvAG4E7gt4AXV9XXd2IXJY25VnH6GbpO5v4J2EKXq36frlO6e+k6bfrYEF7u/wKbgUuB06rqU638JLqTVt+gOzY7b/bVga5l1h50TTI/QHdv8reHEJuWQB56u4I0GkmOBP60qmY2aZIkSdIOSLIW+ArwyJn3/g1h238A/GBVzdbLpkbMK3kaiSSPTXJUa7q0GjiVrjcoSZIk9UySZyT5kXQOBo7HY7fespKnUQldc4S76ZprXk/XBEqSJEn9sztd09H76Zp1ng58YqQRaU4215QkSZKkCeKVPEmSJEmaIGM7GPo+++xTa9eu3ent3H///ey22247H1BPuD/9N2n7NNv+bNq06etV9aQRhdRbi8lb4/I9GZc4wViXyqTEat6a3Xx5q6+ffV/jgv7G1te4oL+x9SWuOXNXVY3l47nPfW4Nw8aNG4eynb5wf/pv0vZptv0Brqwe5Im+PRaTt8blezIucVYZ61KZlFjNW4vPW3397PsaV1V/Y+trXFX9ja0vcc2Vu2yuKUmSJEkTxEqeJEmSJE0QK3mSJEmSNEGs5C2jJPM+JGnapk2bzBWSxorHOFJ/WMmTJEmSpAliJU+SJEmSJoiVPEmSJEmaIFbyJEmSJGmCWMmTJEmSpAliJU+SJEmSJoiVPEmSJEmaIFbyJEmSJGmCWMmTJEmSpAliJU+SJEmSJoiVPEmSJEmaIFbyJEmSJGmCWMmTJEmSpAliJU+SJEmSJoiVPEmSJEmaIFbyJEmSJGmCWMmTJEmSpAliJU/SREpyZpI7klwzUPamJFuTfLE9jhqYd0qSzUluSHL4QPkRrWxzkpMHyvdPcnkrPy/Jo5Zv7yRJkuZmJW9MJJnzIWlWZwFHzFL+jqo6qD0uAkhyIPBy4JltnT9JskuSXYB3A0cCBwLHtGUB/qBt6+nA3cDxS7o3kiRJC2QlT9JEqqrPAHctcPGjgXOr6ttV9RVgM3Bwe2yuqpuq6jvAucDR6c6uvAD4SFv/bOAlQ90BSZKkHbTrqAOQpGX22iTHAlcCb6iqu4HVwGUDy2xpZQC3zig/BHgicE9VPTDL8g+R5ATgBIBVq1YxNTW1oCDXrFnDaaedNuu8hW5jOWzbtq1X8czHWJeGsUpS/1jJk7SSvAd4C1Dt7+nAryzlC1bVGcAZAOvWrav169cvaL3TTz+dk046aa5tDiu8nTY1NcVC92nUjHVpGKsk9Y+VPEkrRlXdPv08yZ8DF7bJrcB+A4uuaWXMUX4nsGeSXdvVvMHlJUmSRsp78iStGEn2HZj8OWC6580LgJcneXSS/YEDgM8BVwAHtJ40H0XXOcsF1V1K2wi8tK1/HPCJ5dgHSZKk7fFKnqSJlOTDwHpgnyRbgFOB9UkOomuueTPwnwCq6tok5wPXAQ8AJ1bVd9t2XgtcDOwCnFlV17aXeCNwbpK3Al8A3rdMuyZJkjQvK3mSJlJVHTNL8ZwVsap6G/C2WcovAi6apfwmut43JUmSesXmmpIkSZI0QXa6ktcGDP5Ckgvb9P5JLk+yOcl57T4W2r0u57Xyy5OsHdjGKa38hiSH72xMo+Sg5ZIkaUck2S/JxiTXJbk2yeta+d5JLklyY/u7VytPkne1Y6irkjxnYFvHteVvTHLcQPlzk1zd1nlXPECRJtIwruS9Drh+YPoPgHdU1dOBu4HjW/nxwN2t/B1tOZIcSNeZwTOBI4A/SbLLEOKSJEkaJw/Qjd95IHAocGI7TjoZuLSqDgAubdMAR9J1FHUA3Xic74GuUkh3H/IhdM3KT52uGLZlfm1gvSOWYb8kLbOdquQlWQO8CHhvmw7wAuAjbZGzgZe050e3adr8F7bljwbOrapvV9VXgM14n4skSVphquq2qvp8e/4NupPoq3noMdTMY6tzqnMZ3dAu+wKHA5dU1V1VdTdwCXBEm/eEqrqs9RJ8zsC2JE2Qne145Y+A3wJ2b9NPBO5p40YBbKFLTrS/twJU1QNJ7m3LrwYuG9jm4DoPkeQEujNVrFq1iqmpqZ0MH7Zt2zaU7Uw77bTTdnjd+eKYb7uD6w17f0Zt0vYHJm+fJm1/JKkP2m0tzwYuB1ZV1W1t1leBVe35g8dWzfQx1HzlW2Ypn/naCzrempn/F3qsstT6/LvU19j6Ghf0N7a+xjVthyt5SV4M3FFVm5KsH15Ic6uqM4AzANatW1fr1+/8y05NTTGM7UzbsGHDDq/bnVRb/HYH1xv2/ozapO0PTN4+Tdr+SNKoJXk88FHg9VV13+Btc1VVSeY+YBiChR5vzcz/Cz1WWWp9/l3qa2x9jQv6G1tf45q2M801nw/8bJKbgXPpmmm+k66pwHTlcQ2wtT3fCuwH0ObvAdw5WD7LOlqAwc5dNm3aZGcvkiSNqSSPpKvgfbCqPtaKb29NLWl/72jlcx1DzVe+ZpZySRNmhyt5VXVKVa2pqrV0Had8uqpeAWwEXtoWOw74RHt+QZumzf90aw9+AfDy1vvm/nQ3AX9uR+OSJEkaR62vgvcB11fVHw7MGjyGmnlsdWzrZfNQ4N7WrPNi4LAke7UOVw4DLm7z7ktyaHutYwe2JWmCLMVg6G8Ezk3yVuALfH/w4fcBH0iyGbiLrmJIVV2b5HzgOrpepU6squ8uQVySNBHmu0q/nE2iJA3d84FXAlcn+WIr+23g7cD5SY4HbgFe1uZdBBxF12ndN4FXA1TVXUneAlzRlntzVd3Vnr8GOAt4LPDJ9pA0YYZSyauqKWCqPb+JWXrHrKpvAb8wx/pvA942jFgkSZLGUVV9FpjrLM4LZ1m+gBPn2NaZwJmzlF8JPGsnwpQ0BoYxTp4kSZIkqSes5EmSJEnSBLGSJ0mSJEkTZCk6XtEOcsgDSZIkSTvLK3mSJEmSNEGs5EmSJEnSBLGSJ0mSJEkTxEqeJEmSJE0QK3mSJEmSNEGs5EmSJEnSBLGSt4IlmfMhjbskZya5I8k1A2V7J7kkyY3t716tPEnelWRzkquSPGdgnePa8jcmOW6g/LlJrm7rvCv+40iSpJ6wkidpUp0FHDGj7GTg0qo6ALi0TQMcCRzQHicA74GuUgicChwCHAycOl0xbMv82sB6M19LkiRpJKzkSZpIVfUZ4K4ZxUcDZ7fnZwMvGSg/pzqXAXsm2Rc4HLikqu6qqruBS4Aj2rwnVNVlVVXAOQPbkiRJGqldRx2AJC2jVVV1W3v+VWBVe74auHVguS2tbL7yLbOUP0ySE+iuDrJq1SqmpqYWFOiaNWs47bTTFrTsoIVuf1i2bdu27K+5o4x1aRirJPWPlTxJK1JVVZJahtc5AzgDYN26dbV+/foFrXf66adz0kkn7cjrLXqdnTE1NcVC92nUjHVpGKsk9Y/NNSWtJLe3ppa0v3e08q3AfgPLrWll85WvmaVckiRp5KzkSVpJLgCme8g8DvjEQPmxrZfNQ4F7W7POi4HDkuzVOlw5DLi4zbsvyaGtV81jB7YlSZI0UjbXlDSRknwYWA/sk2QLXS+ZbwfOT3I8cAvwsrb4RcBRwGbgm8CrAarqriRvAa5oy725qqY7c3kNXQ+ejwU+2R6SJEkjZyVPs5pvyK/lvudH2hFVdcwcs144y7IFnDjHds4Ezpyl/ErgWTsToyRJ0lKwuaYkSZIkTRAreZIkSZI0QazkSZIkSdIEsZInSZIkSRPESp4kSZIkTRB719Si2fOmJEmS1F9eyZMkSZKkCWIlT5IkSZImiJU8SZIkSZog3pM34ea7f06SJEnS5NnhK3lJ9kuyMcl1Sa5N8rpWvneSS5Lc2P7u1cqT5F1JNie5KslzBrZ1XFv+xiTH7fxuSZIkjZckZya5I8k1A2VDO65K8twkV7d13hXPBEsTa2eaaz4AvKGqDgQOBU5MciBwMnBpVR0AXNqmAY4EDmiPE4D3QJe8gFOBQ4CDgVOnE5gkSdIKchZwxIyyYR5XvQf4tYH1Zr6WpAmxw5W8qrqtqj7fnn8DuB5YDRwNnN0WOxt4SXt+NHBOdS4D9kyyL3A4cElV3VVVdwOXYNKRJEkrTFV9BrhrRvFQjqvavCdU1WXVjXd0zsC2JE2YodyTl2Qt8GzgcmBVVd3WZn0VWNWerwZuHVhtSyubq3y21zmB7mwVq1atYmpqaqdj37Zt21C2M+20004b2rZ2xJo1a0Yaw3zv5aZNm+ac99znPnfW8mF/Pn0wafs0afsjST0zrOOq1e35zPKHWejx1sz8P9/xx3L+TvT5d6mvsfU1LuhvbH2Na9pOV/KSPB74KPD6qrpvsHl3VVWSoY2OXVVnAGcArFu3rtavX7/T25yammIY25m2YcOGoW1rR5x22mmcdNJJI3v9+QZDn++9mWu9YX8+fTBp+zRp+yNJfTXs46p5XmdBx1sz8/+O/M4vhT7/LvU1tr7GBf2Nra9xTdupIRSSPJKugvfBqvpYK769NQmg/b2jlW8F9htYfU0rm6tckiRppRvWcdXW9nxmuaQJtDO9awZ4H3B9Vf3hwKwLgOmenI4DPjFQfmzrDepQ4N7W/OBi4LAke7Ubgw9rZZIkSSvdUI6r2rz7khzajuGOHdiWpAmzM801nw+8Erg6yRdb2W8DbwfOT3I8cAvwsjbvIuAoYDPwTeDVAFV1V5K3AFe05d5cVTNvOpYkSZpoST4MrAf2SbKFrpfMYR5XvYauB8/HAp9sD0kTaIcreVX1WWCu8VVeOMvyBZw4x7bOBM7c0VgkSZLGXVUdM8esoRxXVdWVwLN2JkZJ42Gn7smTpHGU5OY2IPAXk1zZyoY24LAkSdIoWcmTtFJtqKqDqmpdmx7mgMOSpAFJ5nxIGj4reTvARCVNpKEMOLzcQUuSJM00lMHQJWnMFPCpNt7Un7UxoYY14PBDLHRQ4ZnWrFkz78DCc1nugVn7PhjsIGNdGsYqSf1jJU/SSvTjVbU1yQ8AlyT50uDMYQ44vNBBhWc6/fTTOemkk4YRwmAsQ90e9H8w2EHGujSMVZL6x+aaGiqbsmocVNXW9vcO4ON099QNa8BhSZKkkbKSp16Yq2K4adOmUYemCZNktyS7Tz+nGyj4GoY04PAy7ookSdKsbK45B688SRNrFfDx9j++K/ChqvqbJFcwvAGHJUmSRsZKnqQVpapuAn50lvI7GdKAw5IkSaNkc01JkiRJmiBW8iRJkiRpgljJkyRJkqQJYiVPkiRJkiaIlTxJkiRJmiBW8iRJkiRpgljJkyRJkqQJYiVPkiRJkiaIlTxJkiRJmiBW8iRJkiRpguw66gAkScsjyZzzqmoZI5EkSUvJK3mSJEmSNEG8kidJkqSRsZWBNHxeyZMkSZKkCWIlT5IkSZImiM01JUk2l5IkaYKs6Ct5Sdi0aRNJHvaQJEmSpHG0oit5kiRJkjRprORJkuY1W2sHWz1IWg7mH2nH9KaSl+SIJDck2Zzk5FHHo/Fg8tcombckjSNzlzT5elHJS7IL8G7gSOBA4JgkB442KvXFjlbklmI9K5WaZt7qzHVfs/8TUj9NUu6aK/ds2rRp1KFJI9eLSh5wMLC5qm6qqu8A5wJHD2PDHpRrNkvxvVhoZXC+g2K/o2NlyfLWpPCEidRLKyJ3mX+00qUPXWMneSlwRFX9apt+JXBIVb12xnInACe0yR8GbhjCy+8DfH0I2+kL96f/Jm2fZtufp1bVk0YRzHJZhrw1Lt+TcYkTjHWpTEqsE5+3YGG5axF5q6+ffV/jgv7G1te4oL+x9SWuWXPXWI2TV1VnAGcMc5tJrqyqdcPc5ii5P/03afs0afszbDuat8blfR2XOMFYl4qxTp6F5q2+vp99jQv6G1tf44L+xtbXuKb1pbnmVmC/gek1rUyS+sq8JWkcmbukFaAvlbwrgAOS7J/kUcDLgQtGHJMkzce8JWkcmbukFaAXzTWr6oEkrwUuBnYBzqyqa5fp5Yfa/LMH3J/+m7R9mrT9WZBlyFvj8r6OS5xgrEvFWMfIkHNXX9/PvsYF/Y2tr3FBf2Pra1xATzpekSRJkiQNR1+aa0qSJEmShsBKniRJkiRNkBVVyUuyX5KNSa5Lcm2S17XyvZNckuTG9nevUce6UEl2SfKFJBe26f2TXJ5kc5Lz2k3VYyPJnkk+kuRLSa5P8rwx/3z+a/uuXZPkw0keM26fUZIzk9yR5JqBslk/k3Te1fbtqiTPGV3k4ynJEUluaO/hySOKYSifeZLj2vI3JjluiWJdVF4fZbzt//9zSf6hxfr7rXzWnJDk0W16c5u/dmBbp7TyG5IcPuxY22ss6Pdl1HG217k5ydVJvpjkylbWu+/ApOhDnhqIZcH5apnj6u0x52Jz0Qji6+Wx7WLyTC9U1Yp5APsCz2nPdwf+ETgQ+J/Aya38ZOAPRh3rIvbpvwEfAi5s0+cDL2/P/xT49VHHuMj9ORv41fb8UcCe4/r5AKuBrwCPHfhsXjVunxHwE8BzgGsGymb9TICjgE8CAQ4FLh91/OP0oOsE4cvA09r3/x+AA8fxMwf2Bm5qf/dqz/daglgXlddHGW97zce3548ELm8xzJoTgNcAf9qevxw4rz0/sH03Hg3s374zuyzBe7ug35dRx9le62ZgnxllvfsOTMKjL3lqIJ4F56tljqu3x5yLzUUjiK+Xx7aLyTN9eIw8gJHuPHwC+GngBmDfVrYvcMOoY1tg/GuAS4EXABe2f9qvA7u2+c8DLh51nIvYnz3oKkWZUT6un89q4NZ2wLBr+4wOH8fPCFg74wd01s8E+DPgmNmW87Gg9/kh3wfgFOCUcfzMgWOAPxsof8hySxj3vHm9L/ECjwM+DxwyV06g6/3wee35rm25zPxeDC43xPgW/PsyyjgHtn0zDz/46vV3YFwffcpTAzEsKF+NOMZeHnMuJBctczy9PbZdTJ7pw2NFNdcc1JqTPJvu7MWqqrqtzfoqsGpEYS3WHwG/BXyvTT8RuKeqHmjTW+gqGuNif+BrwPvbZfr3JtmNMf18qmorcBrwT8BtwL3AJsb7M5o212cyXbGdNq77Nyp9fv8W+5kv+74sMK+PNN7WDOmLwB3AJXRXRObKCQ/G1ObfS5fnlyPWxfy+jDLOaQV8KsmmJCe0sl5+BybAOLxPvTpu6OMx5yJz0XLq87HtYvLMyK3ISl6SxwMfBV5fVfcNzquuKt77cSWSvBi4o6o2jTqWIdqVrsnFe6rq2cD9dJe+HzQunw9Aa5d9NF3l9cnAbsARIw1qCYzTZ6Lh6ONnPi55vaq+W1UH0Z2tPhh4xohDepgx/X358ap6DnAkcGKSnxic2afvgJbXqD/7vuamPuaiMcg9Y5VnVlwlL8kj6f7ZPlhVH2vFtyfZt83fl+6sRt89H/jZJDcD59Jd1n4nsGeS6UHu1wBbRxPeDtkCbKmqy9v0R+gqfeP4+QD8FPCVqvpaVf0r8DG6z22cP6Npc30mW4H9BpYb1/0blT6/f4v9zJdtXxaZ10ceL0BV3QNspGt6NFdOeDCmNn8P4M5liHWxvy+jivNBreUEVXUH8HG6g9ZefwfG2Di8T704bhiHY84F5qLl0utj20XmmZFbUZW8JAHeB1xfVX84MOsC4Lj2/Di6dtO9VlWnVNWaqlpLd6P7p6vqFXT/qC9ti43Fvkyrqq8Ctyb54Vb0QuA6xvDzaf4JODTJ49p3b3p/xvYzGjDXZ3IBcGzrve5Q4N6BZgzaviuAA1pPYo+i+9++YMQxTVvsZ34xcFiSvdpV7cNa2VDtQF4fWbxJnpRkz/b8sXT351zP3DlhcB9eSpfnq5W/PF2vlvsDBwCfG1acO/D7MpI4pyXZLcnu08/pPrtr6OF3YEL0OU9NG/lxQ5+POXcgFy2LPh/b7kCeGb1R3xS4nA/gx+kuo14FfLE9jqJr73spcCPwt8Deo451kfu1nu/3QPQ0uh/RzcBfAo8edXyL3JeDgCvbZ/RXdD2cje3nA/w+8CW6RPABul7mxuozAj5Md0/hv9JdbT1+rs+E7gbpd9O17b8aWDfq+Mft0XLSP7b38HfG+TMHfqV9zzcDr16iWBeV10cZL/AjwBdarNcAv9fKZ80JwGPa9OY2/2kD2/qdtg83AEcu4Xdhu78vo46zxfUP7XHt9P9NH78Dk/LoQ54aiGXB+WqZ4+rtMedic9GIPtft5p5ljmdReaYPj7QAJUmSJEkTYEU115QkSZKkSWclT8sqSSV5+qjjkKRhSbItydNGHYckSdN23f4ikiRpLlX1+FHHIEl9k+Qsul7Tf3fUsaxEXsmTJK1oA11zS5LoegdNMmc9wbzZf1bytNOS3JzklCTXJbk7yfuTPKbN+80ktyX55yS/MmO9FyX5QpL7ktya5E0D8/46yX+ZsfxVSX6uJZ53JLmjrXt1kmcty85KGhtz5aYk65NsSfLGJF8F3p/kEUlOTvLlJHcmOT/J3m07n0zy2hnb/ockP9+eP9gMPckeSc5J8rUktyT53ekDpSRvSvIXA9tY29bdtU2/KslNSb6R5CtJXrFMb5WkJZDkyUk+2vLBV5L8Rit/U5K/TPIX7f/96iQ/1PLVHe2Y6LCB7Uwl+R9JPteOez4xnZ9mvN6jk9wzeEzUhkv4lyQ/0IYHubDFc3d7vmbG67wtyd8B36TrUXJ63nS+Oj7JPwGfbuV/meSrSe5N8pkkz2zlJwCvAH6rNWn/P/O9Jxo+K3kallcAhwP/Bvgh4HeTHAGcRDf+ygF0g4MPuh84FtgTeBHw60le0uadDfzy9IJJfhRYDfw13dgkP9FeZw/gZXQD70rSTA/LTa38B4G9gacCJwD/BXgJ8JPAk4G76brZh66L9mOmN5jkwLbeX8/yev+bLi89rW3rWODV2wsy3bhL76IbZmB34N/TdQeVi7gAACAASURBVLkuaQy1kzv/h67L/dV0Y+W+PsnhbZGfoRtaaS+64QwupjsuXw28GfizGZs8lm6Ij32BB+jyxUNU1beBjzGQr+iOkf5vdQN4PwJ4P13+egrwL8Afz9jMK+ly4u7ALbPs2k8C/5YurwJ8ku4Y7weAzwMfbLGc0Z7/z6p6fFX9zALeEw2RlTwNyx9X1a1VdRfwNroE8zLg/VV1TVXdD7xpcIWqmqqqq6vqe1V1Fd2B1E+22RcAP5TkgDb9SuC8qvoO3Vg4uwPPAFJV15cDbkua3Wy5CeB7wKlV9e2q+hfgP9ONe7SlHSi9CXhpu8r2ceCgJE9t674C+Fhb7kFJdqEbwPeUqvpGVd0MnE6Xvxbie8Czkjy2qm6rqmt3dKcljdyPAU+qqjdX1Xeq6ibgz+lyBMD/q6qLq+oBurHfngS8var+FTgXWJs2YHnzgYHjqf8PeFnLOTN9aOA1AH6plVFVd1bVR6vqm1X1Dbqc+JMz1j+rqq6tqgdaLDO9qarub3mTqjqz5bvpvPmjSfbYwfdEQ2QlT8Ny68DzW+jOhD95lvIHJTkkycZ2yf5euoOsfQCq6lvAecAvtzM/x9Cd8aKqPk135undwB1JzkjyhKXZLUljbrbcBPC1lmemPRX4eGvqdA9wPfBdYFU7GPprvn8gcgztbPUM+wCP5KG57ha6M9bzagduv0iXB29L12T9GdtbT1JvPRV48nROaXnlt4FVbf7tA8v+C/D1qvruwDTAYKdOM3PZI2nHTDNsBB7XjrHWAgfRnagiyeOS/FlrSn4f8BlgzxmVxVtnbnCGB+cn2SXJ21sz9/uAm9us2eKC7b8nGiIreRqW/QaePwX4Z+C2WcoHfYjuit1+VbUH8KdABuafTXfG/IXAN6vq76dnVNW7quq5wIF0TbB+c0j7IWmyzJabAGrGcrfSNZXcc+DxmKra2uZ/GDgmyfOAx9AdSM30dbqWBk8dKHsKML2N+4HHDcz7wcGV21n9n6ZrjvUlujPcksbTrcBXZuSU3avqqB3c3sxc9q90OechWkXxfLqTUccAF7YTVQBvAH4YOKSqnkB36ws89NhrZm582EsMPP8l4Gi623H2ANbO2N5seXaY74nmYSVPw3JikjXtRuDfobsKdz7wqiQHJnkccOqMdXYH7qqqbyU5mC5ZPKhV6r5H19zpA9PlSX6snaF6JN1B07facpI002y5aTZ/Crxtuklm66zg6IH5F9FV3t5M13T8YTln4ODqbUl2b9v6b8B0ZytfBH4iyVNac6ZTptdNsirJ0e3evG8D2zCvSePsc8A30nXw9Nh21etZSX5sB7f3ywPHU28GPjJw5W+mD9G1DHhFez5td7qrhPe0nDjzuGyxdqfLV3fSncD67zPm385A5y0M/z3RPKzkaVg+BHwKuAn4MvDWqvok8Ed0PTBtbn8HvQZ4c5JvAL9Hd3A00znAv+P7B0kAT6A7w303XZOFO4H/NbQ9kTRJHpab5ljunXQtCz7VctJlwCHTMwc6NPgpHnrQNNN/oTv5dBPw2bbsmW0bl9BVMq8CNgEXDqz3CLoK4T8Dd9HdJ/PrC99NSX3SKmAvpmsu+RW6q27vpbvitSM+AJwFfJWuNcGDvVK23iv/w8BrX06Xh55M1zHKtD8CHttiuQz4m/leMF3Pwr89zyLn0B2HbQWua9sc9D7gwNY086+W4D3RPFK1vauy0vyS3Az8alX97RJs+1jghKr68WFvW9JkW8rcJEnLJckU8BdV9d5Rx6Lx4ZU89VZrkvAa4IxRxyJJkiSNCyt56qU2ZsrX6Npzz9c0SpIkSdIAm2tKkiRJ0gTxSp4kSZIkTZBdRx3Ajtpnn31q7dq1213u/vvvZ7fddlv6gIZgXGI1zuEbl1gXGuemTZu+XlVPWoaQxspC8xaMz3diWNzfydf3fTZvzW4xeWsY+v49mcl4l9a4xQvLH/NcuWtsK3lr167lyiuv3O5yU1NTrF+/fukDGoJxidU4h29cYl1onEluWfpoxs9C8xaMz3diWNzfydf3fTZvzW4xeWsY+v49mcl4l9a4xQvLH/NcuWvBzTXbgIVfSHJhm94/yeVJNic5L8mjWvmj2/TmNn/twDZOaeU3tI41psuPaGWbk5y8ozspSZIkSSvdYu7Jex1w/cD0HwDvqKqn0w1KfXwrPx64u5W/oy1HkgOBlwPPBI4A/qRVHHcB3g0cCRwIHNOWlSRJkiQt0oIqeUnWAC+iG5WeJAFeAHykLXI28JL2/Og2TZv/wrb80cC5VfXtqvoKsBk4uD02V9VNVfUd4Ny2rCRJkiRpkRZ6T94fAb8F7N6mnwjcU1UPtOktwOr2fDVwK0BVPZDk3rb8auCygW0OrnPrjPJDZgsiyQnACQCrVq1iampqu4Fv27ZtQcv1wbjEapzDNy6xjkuckiRJK9l2K3lJXgzcUVWbkqxf+pDmVlVnAGcArFu3rhZyU+M43bA5LrEa5/D1KdbuwvvsNm7c2Js4J92mTZvYsGHDrPMc31SSpPE23/HWMH7nF3Il7/nAzyY5CngM8ATgncCeSXZtV/PWAFvb8luB/YAtSXYF9gDuHCifNrjOXOWSJEmSpEXY7j15VXVKVa2pqrV0Had8uqpeAWwEXtoWOw74RHt+QZumzf90ddXRC4CXt9439wcOAD4HXAEc0HrrfFR7jQuGsneSJEmStMLszDh5bwTOTfJW4AvA+1r5+4APJNkM3EVXaaOqrk1yPnAd8ABwYlV9FyDJa4GLgV2AM6vq2p2IS5IkSZJWrEVV8qpqCphqz2+i6xlz5jLfAn5hjvXfBrxtlvKLgIsWE4skSZIk6eEWM06eJEmSlkiSM5PckeSagbI3Jdma5IvtcdTAvFOSbE5yQ5LDB8qPaGWbk5w8UL5/kstb+XntNhlJE8hKniRJUj+cBRwxS/k7quqg9rgIIMmBdLfEPLOt8ydJdkmyC/Bu4EjgQOCYtizAH7RtPR24Gzh+SfdG0shYyZMkSeqBqvoMXX8GC3E0cG5VfbuqvgJspruN5mBgc1XdVFXfAc4Fjk7XX/sLgI+09c8GXjLUHZDUGzvT8YokSZKW3muTHAtcCbyhqu4GVgOXDSyzpZUB3Dqj/BDgicA9beirmcs/RJITgBMAVq1axdTU1JB2Y/u2bdu2rK+3s4x3aY1bvLDwmE877bQ55w1jn63kSZIk9dd7gLcA1f6eDvzKUr5gVZ0BnAGwbt26Wr9+/VK+3ENMTU2xnK+3s4x3aY1bvLDwmDds2DDnvOUaDF2SJEkjUFW3Tz9P8ufAhW1yK7DfwKJrWhlzlN8J7Jlk13Y1b3B5SRPGe/IkSZJ6Ksm+A5M/B0z3vHkB8PIkj06yP3AA8DngCuCA1pPmo+g6Z7mguksDG4GXtvWPAz6xHPsgafl5JU+SJKkHknwYWA/sk2QLcCqwPslBdM01bwb+E0BVXZvkfOA64AHgxKr6btvOa4GLgV2AM6vq2vYSbwTOTfJW4AvA+5Zp1yQtMyt5kiZOkscAnwEeTZfnPlJVp7az3efSdUCwCXhlVX0nyaOBc4Dn0jVp+sWqurlt6xS6bsa/C/xGVV3cyo8A3kl3EPXeqnr7Mu6ipAlUVcfMUjxnRayq3ga8bZbyi4CLZim/ia73TUkTzuaakibRt4EXVNWPAgcBRyQ5lLnHiDoeuLuVv6Mtt6PjUEmSJI2UlTxJE6c629rkI9ujmHuMqKPbNG3+C9uYUosah2qJd0uSJGlBbK4paSK1q22bgKfTXXX7MnOPEbWaNq5UVT2Q5F66Jp2LHYdqtjh2aLypNWvWzDmGzriNGbQQ4zgW0s5YafsLK3OfJWlUrORJmkitA4KDkuwJfBx4xoji2KHxpk4//XROOumkubY5rPB6YxzHQtoZK21/YWXusySNis01JU20qrqHrtvw59HGiGqzBseIenC8qTZ/D7oOWOYah2q+8akkSZJGykqepImT5EntCh5JHgv8NHA9c48RdUGbps3/dBtTalHjUC39nkmSJG2fzTUlTaJ9gbPbfXmPAM6vqguTXMfsY0S9D/hAks3AXXSVth0dh0qSJGmkrORJmjhVdRXw7FnKZx0jqqq+BfzCHNta1DhUkiRJo7bd5ppJHpPkc0n+Icm1SX6/le+f5PIkm5Oc15os0Zo1ndfKL0+ydmBbp7TyG5IcPlB+RCvbnOTk4e+mJEmSJK0MC7knz0GFJUmSJGlMbLeS56DCkiRJkjQ+FnRP3jgPKjxOg6+OS6zGOXx9inWuAbihX3FKkiRpdguq5I3zoMLjNPjquMRqnMPXp1g3bNgw57yNGzf2Jk5JkiTNblHj5DmosCRJkiT120J613RQYUmSJEkaEwtprumgwpIkSZI0JrZbyXNQYUmSJEkaH4u6J0+SJEmS1G9W8iRJkiRpgljJkyRJkqQJYiVPkiRJkiaIlTxJkiRJmiBW8iRJkiRpgljJkyRJ6oEkZya5I8k1A2V7J7kkyY3t716tPEnelWRzkquSPGdgnePa8jcmOW6g/LlJrm7rvCtJlncPJS0XK3mSJEn9cBZwxIyyk4FLq+oA4NI2DXAkcEB7nAC8B7pKIXAqcAjdeManTlcM2zK/NrDezNeSNCGs5EmSJPVAVX0GuGtG8dHA2e352cBLBsrPqc5lwJ5J9gUOBy6pqruq6m7gEuCINu8JVXVZVRVwzsC2JE2YXUcdgCRJkua0qqpua8+/Cqxqz1cDtw4st6WVzVe+ZZbyh0lyAt3VQVatWsXU1NTO7cEibNu2bVlfb2cZ79Iat3hh4TGfdtppc84bxj5byZMkSRoDVVVJahle5wzgDIB169bV+vXrl/olHzQ1NcVyvt7OMt6lNW7xwsJj3rBhw5zzuovtO8fmmpIkSf11e2tqSft7RyvfCuw3sNyaVjZf+ZpZyiVNICt5kiZOkv2SbExyXZJrk7yuldtLnaRxcwEwnXuOAz4xUH5sy1+HAve2Zp0XA4cl2avluMOAi9u8+5Ic2vLVsQPbkjRhrORJmkQPAG+oqgOBQ4ETkxyIvdRJ6rEkHwb+HvjhJFuSHA+8HfjpJDcCP9WmAS4CbgI2A38OvAagqu4C3gJc0R5vbmW0Zd7b1vky8Mnl2C9Jy8978iRNnHbG+rb2/BtJrqfrYOBoYH1b7GxgCngjA73UAZclme6lbj2tlzqAJNO91E3Reqlr5dO91HnAJGmHVdUxc8x64SzLFnDiHNs5EzhzlvIrgWftTIySxoOVPEkTLcla4NnA5YxRL3Vr1qyZs+etcetpbCHGsQe1nbHS9hdW5j5r5Zivxf4wOtGQFstKnqSJleTxwEeB11fVfYM/wn3vpe7000/npJNOmmubwwqvN8axB7WdsdL2F1bmPkvSqHhPnqSJlOSRdBW8D1bVx1qxvdRJkqSJt91Knr3USRo3LYe8D7i+qv5wYJa91EmSpIm3kCt59lInadw8H3gl8IIkX2yPo7CXOkmStAJs9548e6mTNG6q6rPAXC0C7KVOkiRNtEV1vDKOvdSNU29e4xKrcQ5fn2Kdq0dH6FeckiRJmt2CK3nj2kvdOPXmNS6xGufw9SnWDRs2zDlv48aNvYlTkiRJs1tQ75r2UidJkiRJ42EhvWvaS50kSZIkLUKSOR9LbSHNNad7qbs6yRdb2W/T9Up3fpLjgVuAl7V5FwFH0fU4903g1dD1Updkupc6eHgvdWcBj6XrcMVOVyRJkiRpByykd017qZMkSZKkMbGge/IkSZIkSePBSp4kSZIkTRAreZIkSZI0QazkSZIkSdIEsZInSZIkSRPESp4kSZIkTRAreZIkSZI0QazkSZIkSdIEsZInSZIkSRPESp4kSZIkTRAreZIkSZI0QazkSZIkSdIEsZInSZLUc0luTnJ1ki8mubKV7Z3kkiQ3tr97tfIkeVeSzUmuSvKcge0c15a/Mclxo9ofSUvLSp4kSdJ42FBVB1XVujZ9MnBpVR0AXNqmAY4EDmiPE4D3QFcpBE4FDgEOBk6drhhKmixW8iRJksbT0cDZ7fnZwEsGys+pzmXAnkn2BQ4HLqmqu6rqbuAS4IjlDlrS0tt11AFI0lJIcibwYuCOqnpWK9sbOA9YC9wMvKyq7k4S4J3AUcA3gVdV1efbOscBv9s2+9aqOruVPxc4C3gscBHwuqqqZdk5SStRAZ9KUsCfVdUZwKqquq3N/yqwqj1fDdw6sO6WVjZX+UMkOYHuCiCrVq1iampqiLsxv23bti3r6+2s6XhPO+20OZfp0/6M6/s7TgZjnu97MZ9h7LOVPEmT6izgj4FzBsqmmza9PcnJbfqNPLRp0yF0TZsOGWjatI7uAGtTkgvaGfD3AL8GXE5XyTsC+OQy7JeklenHq2prkh8ALknypcGZVVWtArjTWgXyDIB169bV+vXrh7HZBZmammI5X29nTce7YcOGOZfp0/m/cX1/x8lgzPN9L+YzjO+MzTUlTaSq+gxw14zioTRtavOeUFWXtat35wxsS5KGrqq2tr93AB+nu6fu9paPaH/vaItvBfYbWH1NK5urXNKE2e6VPJs8SZogw2ratLo9n1n+MDva7GnNmjVzNvMYt6YrCzGOTXJ2xkrbX1iZ+zwsSXYDHlFV32jPDwPeDFwAHAe8vf39RFvlAuC1Sc6la51wb1XdluRi4L8PdLZyGHDKMu6KpGWykOaaZ2GTJ0kTZphNm7bzOjvU7On000/npJNOmmubwwqvN8axSc7OWGn7Cytzn4doFfDx7lw6uwIfqqq/SXIFcH6S44FbgJe15S+iO+G+me6k+6sBququJG8BrmjLvbmqZrZ4kDQBtlvJq6rPJFk7o/hoYH17fjYwRVfJe7DJE3BZkukmT+tpTZ4Akkw3eZqiNXlq5dNNnqzkSVoKtyfZt53RXmjTpvUzyqda+ZpZlpekoauqm4AfnaX8TuCFs5QXcOIc2zoTOHPYMUrqlx3teGXZmzzBjjV7GqfmIeMSq3EOX59ina8nqD7FuYOG0rSpnQ2/L8mhdK0QjgX+93LuiCRJ0lx2unfN5Wry1F5r0c2exql5yLjEapzD16dY5+sJauPGjb2Jc3uSfJjuKtw+SbbQNRl/O8Nr2vQavn8/8SexBYIkSeqJHa3k2eRJUq9V1TFzzBpK06aquhJ41s7EKEnSStbuM53VJN5/vpx2dAiF6SZP8PAmT8emcyityRNwMXBYkr1as6fDgIvbvPuSHNp65jx2YFuSJEmSpEVayBAKNnmSJEmSpDGxkN41bfIkSZIkSWNiR5trSpIkSZJ6yEqeJEmSJE0QK3mSJEmSNEGs5EmSJEnSBLGSJ0mSJEkTxEqeJEmSJE0QK3mSJEmSNEG2O06eJGnyJZlzXjcEqiRJGhdeyZMkSZKkCWIlT5IkSZImiM01JUmS1Es2JZd2jFfyJEmSJGmCWMmTJEmSpAlic01JkiTtNJtWSv3hlTxJkiRJmiBeyZMkSZKWiFc4NQoTfyVv06ZNJJn1IUmSJE2SuY57PfZdWXpTyUtyRJIbkmxOcvKo45Gk7TFvSRpH5i5p8vWikpdkF+DdwJHAgcAxSQ4cbVSSNDfz1s6ZeXZ5sNWFpKVj7pJWhl5U8oCDgc1VdVNVfQc4Fzh6xDFJ0nzMW5LGUe9y11wnfDzpI+24vnS8shq4dWB6C3DIzIWSnACc0Ca3JblhAdveB/j6bDN6mDzmjLVnjHP4xiLWDRs2LDTOpy51LD2wlHkLepS7luP1TjrppAf3t4e5eSmMxf/8kPV9n1dC3oIF5K6dyFtzWuj/9WAuGNY2l9hOfa+Xex8W8Ts+cu29GZt4B+x0zIv8Xsyau/pSyVuQqjoDOGMx6yS5sqrWLVFIQzUusRrn8I1LrOMSZ5/sSN6Clfdeu7+TbyXu87ja0bw1DOP2PTHepTVu8UJ/Yu5Lc82twH4D02tamST1lXlL0jgyd0krQF8qeVcAByTZP8mjgJcDF4w4Jkmaj3lL0jgyd0krQC+aa1bVA0leC1wM7AKcWVXXDmnzI2lusIPGJVbjHL5xiXVc4lxyS5y3YOW91+7v5FuJ+9w7y5C7dta4fU+Md2mNW7zQk5hTVaOOQZIkSZI0JH1prilJkiRJGgIreZIkSZI0QSa6kpfkiCQ3JNmc5OQRx7Jfko1JrktybZLXtfK9k1yS5Mb2d69WniTvarFfleQ5yxzvLkm+kOTCNr1/kstbPOe1m7VJ8ug2vbnNX7vMce6Z5CNJvpTk+iTP6+N7muS/ts/9miQfTvKYPrynSc5MckeSawbKFv3+JTmuLX9jkuOWKt6VoE95a6nNlRdXgpk5dpLNlqdHHZP6Lclb2u/MF5N8KsmTRx3TfJL8r/b9virJx5PsOeqY5pPkF1rO/V6SkXf1P5dx+j2c7Xhq1Ca2kpdkF+DdwJHAgcAxSQ4cYUgPAG+oqgOBQ4ETWzwnA5dW1QHApW0aurgPaI8TgPcsc7yvA64fmP4D4B1V9XTgbuD4Vn48cHcrf0dbbjm9E/ibqnoG8KN0MffqPU2yGvgNYF1VPYvuRveX04/39CzgiBlli3r/kuwNnEo3mO7BwKnTFUMtTg/z1lKbKy+uBDNz7CSbLU9L8/lfVfUjVXUQcCHwe6MOaDsuAZ5VVT8C/CNwyojj2Z5rgJ8HPjPqQOYyhr+HZ/Hw46mRmthKHt3B5uaquqmqvgOcCxw9qmCq6raq+nx7/g26H7nVLaaz22JnAy9pz48GzqnOZcCeSfZdjliTrAFeBLy3TQd4AfCROeKcjv8jwAvb8ssR5x7ATwDvA6iq71TVPfTwPaXryfaxSXYFHgfcRg/e06r6DHDXjOLFvn+HA5dU1V1VdTfdj12vEt0Y6VXeWmrz5MWJNjPHTrJ58rQ0p6q6b2ByN6DXvQRW1aeq6oE2eRnd2IO9VVXXV9UNo45jO8bq93CO46mRmuRK3mrg1oHpLfTk4KE1v3s2cDmwqqpua7O+Cqxqz0cZ/x8BvwV8r00/EbhnIIENxvJgnG3+vW355bA/8DXg/a3Z03uT7EbP3tOq2gqcBvwTXeXuXmAT/XxPYfHvX2//18bQin0vZ+TFSTczx06yufK0NK8kb0tyK/AK+n8lb9CvAJ8cdRATYMX+Hg7LJFfyeinJ44GPAq+fcaaK6sazGOnZqiQvBu6oqk2jjGOBdgWeA7ynqp4N3M/3mxYCvXlP96I7+7Q/8GS6s5JjcaWrD++fJt98eXHSjFmOHYbt5mmtTEn+tt2nPvNxNEBV/U5V7Qd8EHjtaKPdfrxtmd+ha4b+wdFF+mAs241Xk60Xg6Evka3AfgPTa1rZyCR5JN2BzAer6mOt+PYk+1bVba3p2x2tfFTxPx/42SRHAY8BnkB3P8WeSXZtV5YGY5mOc0trirgHcOcyxAndWZ0tVTV95v8jdAcPfXtPfwr4SlV9DSDJx+je5z6+p7D4928rsH5G+dQyxDmJepe3ltoceXGSPSzHJvmLqvrlEce1VObK01rhquqnFrjoB4GL6O79HpntxZvkVcCLgRdWDwahXsT721cr7vdw2Cb5St4VwAHpejB8FF1HFxeMKph2T9X7gOur6g8HZl0ATPdGeBzwiYHyY9M5FLh3oAndkqmqU6pqTVWtpXvPPl1VrwA2Ai+dI87p+F/all+W5FZVXwVuTfLDreiFwHX07D2la6Z5aJLHte/BdJy9e09nef2FvH8XA4cl2atdtTyslWnxepW3lto8eXFizZFjJ7WCN1+eluaU5ICByaOBL40qloVIcgRdE+yfrapvjjqeCbGifg+XRFVN7AM4iq6Xoy8DvzPiWH6crtnbVcAX2+MounutLgVuBP4W2LstH7pehb4MXE3XM+Nyx7weuLA9fxrwOWAz8JfAo1v5Y9r05jb/acsc40HAle19/Stgrz6+p8Dv0/1IXQN8AHh0H97T/7+9uw+XrCzvfP/9BXwL6gCirdJok4g5QeZooAfIFTOnOybQMkZMxjgQldagJFEmMQmJqDlBRedo0sToxGgwMoBRgTFRiMEgY9jjlcyA0IgKvgwtQqBFUBrBFqOi9/ljPRuKza79Wruqdu3v57rq6lXPeqm7VlU/u+61nhfgg3T9BL9Pd8X9xKWcP7o+CDva46XD/q5O0mOc6q0hvNdZ68VRxzXE939fHTvJj9nq6VHH5GO8H3R3969t35m/A/YfdUzzxLuDrv/YdD327lHHNE+8v9T+5n8XuA24ZNQx9Ylz1fw9nO331KhjSgtMkiRJkjQBJrm5piRJkiStOSZ5kiRJkjRBTPI0dpJ8LMnW+bcczDGTbEhSbSRLSVpxSX4myfVJdid53ox11yXZ1Ge/TUluGUqQklaN3nojyeuT/PWIQ9KI+aNWY6eqnr0ajilJy/BG4M+r6u0zV1TV00YQj6RVbCXrjSS/A/xnYD9gN3A+8PvVTQGlMeWdPI2NNjS/30lJa8GTgetGHYSk1W2lWyEl2YNu6oJDq+rRwCHA04HfWsnX1fL5g3qNSHJAkr9N8vUkdyT58yQ/kuQPk9yU5PYk5yb5N2376SaMW5P8S5JvJHldz/EOT3JVkruT3JZk1jmukrwkyT+317sryReTPKtn/VSSNyf5Z+Ae4Mda2ct6tnl5ki8k+VaSzyc5tJU/McnftPf0lSR9K5zeYybZI8m29p5uAP5Dz3b7JrklyS+2549MsiPJCUs89ZIGYFR1WNu2Xx30k61u+WZrKvXcnn3OTvLOJH/f9rsiyY+3dV+mm0Ll71pzzYfNeL0bk/x8W35EO9adST4P/Lue7X48ya4ZdeLX+zX1lDRe+v2Oaf/n39Sz3QOaabc64tVJPgt8O8mevfVG8/Ak57f65+okT+/Zf766611JLk7ybWBzVX25qr45vQnwQ+ApPftUkleka4L+rSSnt/rpf7U69oJ0c91piEzy1oB0V2E+CtwEbAD2B84DXtIem+l+cDwS+PMZuz8T+Am6CWz/KMlPtvK3W6HMNgAAIABJREFUA29vV3V+HLhgjhCOoJvjZD/gNOBvk+zbs/7FwEnAo1qMvbH/CvB64ATg0cBzgTvS3fH7O+Az7f08C3hVkqPnPhsAvBx4DvBTwEbun5CcqtpFN+fbe5I8DngbcE1VnbuA40paAaOsw+aogx5CVwd9HHgcXVOm9+f+Sb+hm7z3DXTzd+4A3gxQVT8O/Avwi1X1yKr67hxv/7QW348DRwP39S2uqi8Drwb+OsmPAv8NOKeqpuY4nqQxsMzfMQDH012k3rtPs8lj6ebc3Rf4APCRJA9ZYN31q3T11aOAf2rx/mqSu4Fv0N3J+8sZr3c0cBhwJN3E8GcCLwIOoLv7d/wC35cGxCRvbTgceCJd++lvV9W/VtU/AS8E/rSqbqiq3cBrgOPywFv/b6iq71TVZ+gqoukrQd8HnpJkv6raXVWXz/H6twN/VlXfr6rzgS/Rc/cMOLuqrquqe6vq+zP2fRnwx1V1ZXV2VNVNdFezH1tVb6yq71XVDcB76H5UzecFLZ6bW1L3//WurKqP01WMn6CbiPPXF3BMSStnlHVYvzroSLqk8i2tDvpHukS094fMh6vqU+0H2PvpJgVfrBcAb66qXVV1M/CO3pVV9R66BPIK4AnA6x58CEljaDm/YwDe0X7HfKfP+u1V9aH2u+pPgYfT1VsLqbsurKp/rqofVtW/AlTVB9pFsacC76abRL3XH1fV3VV1Hd1E9h9vdfNdwMfoLqxriEzy1oYDgJtmudLzRB545+wmusF41vWUfa1n+R66igHgRLr/6F9McmWS58zx+jurqma8zhN7nt88T+xfnqX8ycATW1ODbyb5JvDaGbH388QZr3nTLNucSXfl6eyqumMBx5S0ckZZh/Wrg54I3FxVP5zx+vsv4LUXYyH11Xvo6qv/Os9dQUnjYzm/Y2Du304PWN/qqVvo6pOF1F19j11V19P1J/6LGat6k77vzPJ8KfWflsEkb224GXhSHtw596t0lcy0JwH38uCrMw9SVddX1fF0t/rfCnwoyV59Nt8/SWa8zld7DzdP7D/ep/wrVbV3z+NRVXXMfLEDt9L9cOuN5z6tadiZwLnAK5I8BUmjNMo6rF8d9FXggDxwsKgnATvne+1Fmq++eiTwZ8B7gdfPaAovaXzN9Tvm28CP9mz7+Fn2n+u3E/TUG62eWk9Xby2k7prv2Hsye72oMWKStzZ8iu6HwluS7JXk4Ul+Bvgg8DtJDmw/FP4LcP5ChsRN8qIkj21XgqY74/6wz+aPA36rtQX/FeAngYsXGPtfAackOSydpyR5cntP32odjx+RbjCVQ5L8u3mOB13fm99Ksj7JPsCpM9a/lq6C+zXgT4BzW+InaTRGWYf1q4OuoLs79wetbtsE/CJdX8FBugB4TZJ9kqyn6z/T6+3AVVX1MuDv6ZpRSRp/c/2OuQY4Jt1gcI8HXrWE4x+W5JfbxbFXAd8FLmcJdVeSl7VxCkhyMF3T+E8sISYNkUneGlBVP6D7D/wUus7+twD/CTgLeB/wSeArwL/y4B8Q/WwBrkuym+5HxnHT7cLTjRb3sz3bXgEcRNdZ983A8xfaBLKq/nvb5wPAt4CPAPu29/Qcuj4uX2nH/itgemS9FybpNzz5e4BL6PrnXA387fSKJIcBvwuc0F7jrXQJ38xEUNKQjLIOm6MO+l6L6dl09c9f0NUbX1zs+0vy2iQf67P6DXRNqb5CN1DC+3r2O7a9j99sRb8LHJrkhYuNQdJwzfM75n10v1FupPt/f/4SXuJCunryTroB7n65jY2wlLrrZ4DPpRtt8+L2eO0SYtIQ5YFdpaTBSvIS4GVV9cxRxyJJkiStBd7JkyRJkqQJYpInSZIkSRNk3iQvyVlJbk9ybU/Z65PsTHJNexzTs+41SXYk+VLvhI5JtrSyHUlO7Sk/MMkVrfz8JA8d5BvUaFXV2TbVlCRJkoZnIXfyzqbr2D3T26rqGe1xMdw34s5xwNPaPn/RRgvaA3gnXSfPg4Hj27bQDWzxtqp6Cl3n0BOX84YkSZIkaS2bOefQg1TVJ5NsWODxjgXOa5OxfiXJDuDwtm5HVd0AkOQ84NgkXwB+DvjVts05wOuBd833Qvvtt19t2LDQsFbWt7/9bfbaq98UcePBGAdjNcQIo49z+/bt36iqx44sgDE1qHpr1J/vYhnvyjLewbDemt2wf2+N6/djoYx/tNZi/P3qrnmTvDmcnOQE4Crg96rqTmB/ujk4pt3SyqCb9LG3/AjgMcA3e+Y06t3+QZKcBJwEsG7dOrZt27aM8Adn9+7dPPKRjxx1GHMyxsFYDTHC6OPcvHnzTSN78TG2YcMGrrrqqmUfZ2pqik2bNi0/oCEx3pVlvIORxHprFoOqtxZqXL8fC2X8o7UW4+9Xdy01yXsXcDrd/GGnA2fQTRy9oqrqTOBMgI0bN9a4fIir4QtljIOxGmKE1ROnJOl+Sc6imzvt9qo6pJW9Hng58PW22Wt7usm8hq6byw+A36qqS1r5Frr5H/cA/qqq3tLKD6Sb9PoxwHbgxW3eNEkTZkmja1bVbVX1g6r6Id3E0tNNMncCB/Rsur6V9Su/A9g7yZ4zyiVJktaas3EcBEkDsKQkL8kTep7+EjA98uZFwHFJHtauFh0EfAq4EjiojaT5ULpK6aLqZmK/DHh+238rcOFSYpIkSVrNquqTwK4Fbn7fOAhV9RVgehyEw2njILS7dNPjIIRuHIQPtf3PAZ430DcgaWzM21wzyQeBTcB+SW4BTgM2JXkGXXPNG4FfB6iq65JcAHweuBd4ZVX9oB3nZOASuqYDZ1XVde0lXg2cl+RNwKeB9w7s3UlL0P0dnN1ll102xEgkrTVz1T/ddVGtUUMdB2HmGAhTU1MDehvz271791Bfb9CMf7RWU/zbt29/UNn69es544wzOOyww5Z9/IWMrnn8LMV9E7GqejPw5lnKLwYunqX8Bu5v7ilJkqT7DX0chFGOgbDa+5Qb/2itpvg3b978oLJt27ZxyimnDOSi3nJG15QkSdIKqqrbppeTvAf4aHvab7wD+pTfNw5Cu5vnOAjSBFtSnzxJkiStPMdBkLQU3smTJEkaA46DIGlQTPIkSZLGgOMgSBoUm2tKkiRJ0gQxyZMkSZKkCWKSJ0mSJEkTxCRPkiRJkiaISZ4kSZIkTRCTPEmSJEmaICZ5kiRJkjRBTPIkSZIkaYKY5EmSJEnSBDHJkyRJkqQJYpInSZIkSRPEJE+SJEmSJohJniRJkiRNEJM8SZIkSZogJnmSJEmSNEFM8iRNpCRnJbk9ybU9ZfsmuTTJ9e3ffVp5krwjyY4kn01yaM8+W9v21yfZ2lN+WJLPtX3ekSTDfYeSJEmzM8mTNKnOBrbMKDsV+ERVHQR8oj0HeDZwUHucBLwLuqQQOA04AjgcOG06MWzbvLxnv5mvJUmSNBImeZImUlV9Etg1o/hY4Jy2fA7wvJ7yc6tzObB3kicARwOXVtWuqroTuBTY0tY9uqour6oCzu05liRJ0kjtOeoAJGmI1lXVrW35a8C6trw/cHPPdre0srnKb5ml/EGSnER3d5B169YxNTW1vHcA7N69eyDHGRbjXbht27b1XdcvJs+vJGkmkzxJa1JVVZIawuucCZwJsHHjxtq0adOyjzk1NcUgjjMsxrtwmzdv7ruuu2n8YJ5fSdJMNteUtJbc1ppa0v69vZXvBA7o2W59K5urfP0s5ZIkSSNnkidpLbkImB4hcytwYU/5CW2UzSOBu1qzzkuAo5Ls0wZcOQq4pK27O8mRbVTNE3qOJUmSNFI215Q0kZJ8ENgE7JfkFrpRMt8CXJDkROAm4AVt84uBY4AdwD3ASwGqaleS04Er23ZvrKrpwVxeQTeC5yOAj7WHJEnSyM2b5CU5C3gOcHtVHdLK9gXOBzYANwIvqKo72xXtt9P9WLoHeElVXd322Qr8YTvsm6rqnFZ+GPf/ULoY+O3q1/FAkhaoqo7vs+pZs2xbwCv7HOcs4KxZyq8CDllOjJIkSSthIc01z8a5piRJkiRpVZg3yXOuKUmSJElaPZbaJ2/oc03Bysw3NQirYc4fY1y4ueapGpcY57Na4pQk3c8uMpIGZdkDrwxrrqn2WgOfb2oQVsOcP8a4cHPNU3XZZZeNRYzzGZdzKUlalLOBP6dr2TRtuovMW5Kc2p6/mgd2kTmCrvvLET1dZDYCBWxPclFrSTXdReYKuiRvCw4aJU2kpU6h4FxTkiRJA2QXGUmDstQ7edNzTb2FB881dXKS8+iuKt1VVbcmuQT4Lz2DrRwFvKYNT353m5fqCrq5pv7rEmOSJEmaNEPvIjPK7jGrvbuB8Y/Waop/tu5B69evZ9u2bQN5DwuZQsG5piRJkkZsWF1kRtk9ZrV3NzD+0VpN8c/WPWjbtm2ccsopDKKr7LxJnnNNSZIkjcxtSZ7QWkYttIvMphnlU9hFRlpTltonT5IkSStvuosMPLiLzAnpHEnrIgNcAhyVZJ/WTeYo4JK27u4kR7aROU/oOZakCbPs0TUlSZK0fHaRkTQoJnmSpInQ3ZyYnVOBaTWwi4ykQTHJkyRJkqQBm+vi40qzT54kSZIkTRCTPEmSJEmaICZ5kiRJkjRBTPIkSZIkaYKY5EmSJEnSBDHJkyRJkqQJYpInSZIkSRPEJE+SJEmSJohJniRJkiRNkD1HHYAkSQuVZNQhSJI09ryTJ0mSJEkTxCRPkiRJkiaISZ4kSZIkTRCTPEmSJEmaICZ5kiRJkjRBTPIkSZIkaYI4hcIEmGtI8aoaYiSSJpF1jKRxZN0k9eedPEmSJEmaICZ5kiRJkjRBTPIkSZIkaYKY5Elac5LcmORzSa5JclUr2zfJpUmub//u08qT5B1JdiT5bJJDe46ztW1/fZKto3o/kiRJvUzyJK1Vm6vqGVW1sT0/FfhEVR0EfKI9B3g2cFB7nAS8C7qkEDgNOAI4HDhtOjGUJEkaJZM8SeocC5zTls8BntdTfm51Lgf2TvIE4Gjg0qraVVV3ApcCW4YdtCRJ0kxOoSBpLSrg40kK+MuqOhNYV1W3tvVfA9a15f2Bm3v2vaWV9St/gCQn0d0BZN26dUxNTS07+N27dw/kOAu1bdu2vusWEscg450rlrks5vWHfX57LeVcjzLepVht8UrSarSsJC/JjcC3gB8A91bVxtaE6XxgA3Aj8IKqujPdZCZvB44B7gFeUlVXt+NsBf6wHfZNVXUOkrRynllVO5M8Drg0yRd7V1ZVtQRw2VoCeSbAxo0ba9OmTcs+5tTUFIM4zkJt3ry577qFzEU1yHjnimUui5kza9jnt9dSzvUo412K1RavJK1Gg2iuab8WSatKVe1s/94OfJiu7rmtNcOk/Xt723wncEDP7utbWb9ySRo4B4yStBgr0SfPfi2aVZK+D2lYkuyV5FHTy8BRwLXARcD0D56twIVt+SLghPaj6Ujgrtas8xLgqCT7tB9WR7UySVopXliXtCDL7ZM3tH4tsDJ9WwZh1P0LFtKHY9QxwvxxjkOMMHec4xLjfFZLnCOyDvhwu7iwJ/CBqvqHJFcCFyQ5EbgJeEHb/mK6ZuY76JqavxSgqnYlOR24sm33xqraNby3IUkcC2xqy+cAU8Cr6bmwDlyeZPrC+ibahXWAJNMX1j843LAlrbTlJnlD69fSjjfwvi2DMOr+BQvpwzHqGGH+OMchRpg7zssuu2wsYpzPuJzLcVRVNwBPn6X8DuBZs5QX8Mo+xzoLOGvQMUrSLFb1gFELtZiLlMsdFGolrPaLrMY/WIsdLGz9+vVs27ZtIO9hWUleb7+WJA/o11JVty6iX8umGeVTy4lLkiRpwqzqAaMWajEXKZc7KNRKWO0XWY1/sBY7WNi2bds45ZRTBvL9XXKfPPu1SJIkDYcDRklajOUMvLIO+KcknwE+Bfx9Vf0D8BbgF5JcD/x8ew5dv5Yb6Pq1vAd4BXT9WoDpfi1XYr8WSZKk+3hhXdJiLbm5pv1apNGaa1TSyy67bIiRSJJWmANGSVqU5Q68IkmSpBXkhXVJi7US8+RJkiRJkkbEJE+SJEmSJohJniRJkiRNEPvkaVZzDeoxqrlnJEmSJM3PO3mSJEmSNEFM8iRJkiRpgpjkSZIkSdIEMcmTJEmSpAlikidJkiRJE8TRNSVJkiRNBEeI75jkSZLm/KMoSZJWF5trSpIkSdIE8U7eGuaVe0mSJGnyeCdPkiRJkiaId/IkSZI0URx8Q2udSZ4kSZKWzcRKGh8215QkSZKkCeKdPEmSJK0o7/JJw+WdPEmSJEmaICZ5kiRJkjRBTPIkSZIkaYKY5EmSJEnSBDHJkyRJkqQJYpInSVrTkjzgsX379vuW1d/M89b7kCSN1sRPobDUIXsd6leSJoeJhyRpLZn4JE8aB140kCRJGq219HvM5ppDNFfTFq8yrw69zbj8/DQqfg8101r/27LW3/9q16+5tJ+ftHRjk+Ql2ZLkS0l2JDl11PFI0nyst9TPWk865nr/XqQYPesuafKNRZKXZA/gncCzgYOB45McPNqo+htFJ/3V8oNhnOKc787puMQ5Cmv9/Q/Caqu3NHir5f/RUuvCcXsfGgzrrtXzf1dajrFI8oDDgR1VdUNVfQ84Dzh2xDFJa5J//BZsReut1fI5rJY4Jd1nVf3mGnYd4wWRtWupn++4fi8yDp0Mkzwf2FJVL2vPXwwcUVUnz9juJOCk9vQngC8NNdD+9gO+Meog5mGMg7EaYoTRx/nkqnrsCF9/xY243hr157tYxruyjHcwJr7egoXVXSP+vTWu34+FMv7RWovxz1p3rarRNavqTODMUccxU5KrqmrjqOOYizEOxmqIEVZPnGvBStRbq+3zNd6VZbwatFH+3lrt3w/jHy3jv9+4NNfcCRzQ83x9K5OkcWW9JWk1su6S1oBxSfKuBA5KcmCShwLHAReNOCZJmov1lqTVyLpLWgPGorlmVd2b5GTgEmAP4Kyqum7EYS3G2DUhnYUxDsZqiBFWT5yr1ojrrdX2+RrvyjJeLdgq+M212r8fxj9axt+MxcArkiRJkqTBGJfmmpIkSZKkATDJkyRJkqQJYpI3hyS/neTaJNcleVUr+5MkX0zy2SQfTrJ3n31vTPK5JNckuWoEcZ7eYrwmyceTPLHPvluTXN8eW8c0xh+0ba5JsmKdw2eLsWfd7yWpJPv12Xdk53ERMQ7lPGplJHl9kp09n+ExPetek2RHki8lOXqUcc4083uZZFOSu3rexx+NOsaZZok5Sd7RzvFnkxw66hihfx06rud4jnjH8vxquJKcleT2JNeOOpalSHJAksuSfL79jf7tUce0GEkenuRTST7T4n/DqGNarCR7JPl0ko+OOpalGHjuUFU+ZnkAhwDXAj9KN0DN/wCeAhwF7Nm2eSvw1j773wjsN8I4H92zzW8B755l332BG9q/+7TlfcYpxrZu96jOY1t3AF0H9Ztm+0xHfR4XEuOwzqOPlXsArwdOmaX8YOAzwMOAA4EvA3uMOt4W24O+l8Am4KOjjm2RMR8DfAwIcCRwxajjbHHNWoeO6zmeI96xPL8+hv79+PfAocC1o45lifE/ATi0LT8K+D/AwaOOaxHxB3hkW34IcAVw5KjjWuR7+F3gA+NY/y0w/hv7/YZbysM7ef39JN0fmnuq6l7gfwK/XFUfb88BLqebX2aU+sV5d882ewGzjbBzNHBpVe2qqjuBS4EtYxbjsMwaY1v3NuAP6B/fSM/jAmPU5DoWOK+qvltVXwF2AIePOKZpq/F7OVvMxwLnVudyYO8kTxhJdD3GrA6d1xzxjuX51XBV1SeBXaOOY6mq6taqurotfwv4ArD/aKNauPb/b3d7+pD2GOs6pVeS9cB/AP5q1LGMC5O8/q4FfjbJY5L8KN2VxgNmbPNrdFcfZ1PAx5NsT3LSKOJM8uYkNwMvBGZrrrM/cHPP81tYmQppOTECPDzJVUkuT/K8FYivb4xJjgV2VtVn5th3pOdxgTHCcM6jVtbJrTnbWUn2aWXD+v4tyjzfy59uTYI+luRpw46tnzliHstzDHPWoeN6jmeLd2zPr7QUSTYAP0V3N2zVaM0drwFup7t4vZri/zO6C3Q/HHUgyzDQ3GEs5skbR1X1hSRvBT4OfBu4BvjB9PokrwPuBd7f5xDPrKqdSR4HXJrki+0q1dDirKrXAa9L8hrgZOC0Qb/+kGJ8cjuXPwb8Y5LPVdWXhxDjw4DX0jXRHbkBxLji51HLk+R/AI+fZdXrgHcBp9P9ETgdOIPuQtPIzBNvv+/l1XTfxd3p+hV+BDho5aJ8oCXGPDJzxVtVF/apQ0d2jpcYrzQxkjwS+BvgVTPuXo+9qvoB8Ix04018OMkhVTX2fSSTPAe4vaq2J9k06niWYaC5g3fy5lBV762qw6rq3wN30rWvJslLgOcAL6zWiHaWfXe2f28HPswKNp/qF2eP9wP/cZZdd/LAu5PrW9k4xdh7Lm8Apuiujg0jxuvo+jh9JsmNdOfn6iQzf8CM8jwuNMahnUctXVX9fFUdMsvjwqq6rap+UFU/BN7D/XXK0L5/C42Xrl/qrN/Lqrp7uklQVV0MPCR9Bgsal5gZw3NcVRfO2PS+OnSU53gp8TLC8ysNUpKH0CV476+qvx11PEtVVd8ELmNlup6shJ8Bntvq7vOAn0vy16MNafEGnTuY5M2hZdIkeRJd36cPJNlCdzv4uVV1T5/99kryqOlluivDK3YlpE+cvVdtjwW+OMuulwBHJdmnNf06qpWNTYwttoe15f3o/iN/fkgxnlNVj6uqDVW1ga4J0aFV9bUZu47yPC4oxmGeR62MGX2Ufon765SLgOOSPCzJgXR3bD417Ph6VdXn+n0vkzw+SQCSHE73d+iOEYYLzB0z3Tk+IZ0jgbuq6tZRxgvQrw4d13M8R50/ludXWoz2f+69wBeq6k9HHc9iJXlsu4NHkkcAv8Dsvx3HTlW9pqrWt7r7OOAfq+pFIw5rUVYid7C55tz+JsljgO8Dr6yqbyb5c7omcpe2v6GXV9VvpBsK+q+q6hhgHd1tbujO8Qeq6h+GHOd7k/wEXdvkm4DfAEiyEfiNqnpZVe1KcjpwZTvOG6tqpTo9LylGusFG/jLJD+l+qLylqlYqOXlQjP02HKfzuJAYGe551Mr44yTPoGuueSPw6wBVdV2SC+iS9nvpvhc/6HuU0Xs+8JtJ7gW+AxzXr0XEGLmYrg/sDuAe4KWjDec+b5mtDmV8z3G/eMf1/GqIknyQbmTY/ZLcApxWVe8dbVSL8jPAi4HPpevXBvDadjd9NXgCcE6SPeh+J1xQVatyKoJVauC5Q8aj3pckSZIkDYLNNSVJkiRpgpjkaWwluTHJzw/5NV+/GjvrSpIkSdNM8iRJkiRpgpjkaU5JHJxHkiRJWkVM8tao1hTylCSfTXJXkvOTPDzJpiS3JHl1kq8B/23Gfg9Lsi3JvyS5Lcm721C79Oz7B0luT3JrkuclOSbJ/0myK8lre471+iQfaq/9rSRXJ3l6n3gfluTPkny1Pf6sZ0qAa5P8Ys+2D0nyjSQ/1Z4fmeR/Jflmks+kZ6LMJAcm+Z/t9S8FhjZfl6TVJ8nvJ/mbGWXvSPL2UcUkSdJMJnlr2wvoJro8EPi/gZe08scD+wJPBk6asc9bgKcCzwCeAuwP/FHP+scDD+8pfw/wIuAw4GeB/7fN5TXtWOC/t9f7APCRdJOJzvQ64Mj2uk+nmyDyD9u6c9trTDsGuLWqPp1kf+DvgTe11ziFbhqCx7ZtPwBsp0vuTge2zvLakjTtr4EtPfNJ7Uk3L9O5I41KkqQeJnlr2zuq6qttTre/o0ugoJvD6LSq+m5VfWd64zbR50nA71TVrqr6FvBf6H7gTPs+8Oaq+j5wHl3y9Paq+lZVXUc3l1fv3brtVfWhtv2f0iWIR84S6wvp5p+7vaq+DryBbj4a6H50HZPk0e35i4H3teUXARdX1cVV9cOquhS4qm3/JODfAf9ve6+fbOdBkmbVJun+JPArrWgL8I2q2j66qCRJeiCTvLXtaz3L9wCPbMtfr6p/nWX7xwI/CmxvTR+/CfxDK592R89EzNMJ4m0967/T8zoAN08vVNUPgVuAJ87y2k+kmzx32k3T21XVV4F/Bv5ju7r+bOD9bbsnA78yHW+L+Zl0k34+Ebizqr4947iSNJdzuL/1wIu4/6KSJEljwUE1NJvqU/4NuiTtaVW1c0CvdcD0QpIfAdYDX51lu6/SJWzXtedPmrHdOcDL6L7T/7snvpuB91XVy2ceMMmTgX2S7NWT6D2J/u9fkgA+ArwrySHAc4A/GHE8kiQ9gHfytGDtTtt7gLcleRxAkv2THL2Mwx6W5Jdbv5ZXAd8FLp9luw8Cf5jksUn2o+vv1zuf3UeAQ4Hf5oF9Y/4a+MUkRyfZo2dwmfVVdRNd0803JHlokmcCv4gkzaG1dPgQXZ/eT1XVv4w4JEmSHsAkT3NK8rNJdvcUvRrYAVye5G7gfwA/sYyXuBD4T8CddH3pfrn1z5vpTXQJ2WeBzwFXtzIAWt/Bv6EbROZve8pvphvc5bXA1+nu7P0+93/3fxU4AtgFnIaDJ0hamHOAf4tNNSVJYyhVtkzTaCR5PfCUqnrRfNsu8Hh/BDx1UMeTpH7awE1fBB5fVXePOh5JknrZJ08TIcm+wIncP+KmJK2I1n/4d4HzTPAkSePI5ppa9ZK8nK4Z5sfaNAiStCKS7AXcDfwCXRNvSZLGjs01JUmSJGmCeCdPkiRJkibIqu2Tt99++9WGDRtGHcasvv3tb7PXXnuNOoy+jG95jG9+27dv/0ZVPXakQYyhxdRb4/A5LoRxDtZqiRNWT6wLjdN6S9IkWbVJ3oYNG7jqqqtGHcaspqam2LRp06jD6Mv4lsf45pfkppEGMKYWU2+Nw+e4EMY5WKslTlg9sS40TustSZPE5pqSJEmSNEFM8iRJkiSiKanfAAAUyklEQVRpgpjkSZIkSdIEMcmT9ABJ+j40PNu3b/dzkCRJS2KSJ0mSJEkTxCRPkiRJkiaISZ4kSZIkTRCTPEmSJEmaIPMmeUnOSnJ7kmt7yl6fZGeSa9rjmJ51r0myI8mXkhzdU76lle1IcmpP+YFJrmjl5yd56CDfoCRJkiStJQu5k3c2sGWW8rdV1TPa42KAJAcDxwFPa/v8RZI9kuwBvBN4NnAwcHzbFuCt7VhPAe4ETlzOG5IkSZKktWzeJK+qPgnsWuDxjgXOq6rvVtVXgB3A4e2xo6puqKrvAecBx6YbC/zngA+1/c8BnrfI9yBJkiRJavZcxr4nJzkBuAr4vaq6E9gfuLxnm1taGcDNM8qPAB4DfLOq7p1l+wdJchJwEsC6deuYmppaRvgrZ/fu3WMbGxjfck16fNu2beu7bpzftyRJkjpLTfLeBZwOVPv3DODXBhVUP1V1JnAmwMaNG2vTpk0r/ZJLMjU1xbjGBsa3XJMe3+bNm/uuq6olH1eSJEnDsaQkr6pum15O8h7go+3pTuCAnk3XtzL6lN8B7J1kz3Y3r3d7SZIkSdIiLWkKhSRP6Hn6S8D0yJsXAccleViSA4GDgE8BVwIHtZE0H0o3OMtF1d0WuAx4ftt/K3DhUmKSJEmSJC3gTl6SDwKbgP2S3AKcBmxK8gy65po3Ar8OUFXXJbkA+DxwL/DKqvpBO87JwCXAHsBZVXVde4lXA+cleRPwaeC9A3t3kiRJkrTGzJvkVdXxsxT3TcSq6s3Am2cpvxi4eJbyG+hG35QkSZIkLdOSmmtKkiRJksaTSZ4kSZIkTRCTPEkTJ8nDk3wqyWeSXJfkDa38wCRXJNmR5Pw2EBRtsKjzW/kVSTb0HOs1rfxLSY7uKd/SynYkOXXY71GSJKkfkzxJk+i7wM9V1dOBZwBbkhwJvBV4W1U9BbgTOLFtfyJwZyt/W9uOJAfTjQb8NGAL8BdJ9kiyB/BO4NnAwcDxbVtJkqSRM8mTNHGqs7s9fUh7FPBzwIda+TnA89ryse05bf2zkqSVn1dV362qrwA76AaKOhzYUVU3VNX3gPPatpIkSSO3pMnQJWnctbtt24Gn0N11+zLwzaq6t21yC7B/W94fuBmgqu5NchfwmFZ+ec9he/e5eUb5EX3iOAk4CWDdunVMTU0tKP7169ezbdu2Wdct9BjDsHv37rGKpx/jHLzVEutqiVOSBskkT9JEanN0PiPJ3sCHgf9rRHGcCZwJsHHjxtq0adOC9jvjjDM45ZRT+h1zUOEt29TUFAt9T6NknIO3WmJdLXFK0iDZXFPSRKuqbwKXAT8N7J1k+uLWemBnW94JHADQ1v8b4I7e8hn79CuXJEkaOZM8SRMnyWPbHTySPAL4BeALdMne89tmW4EL2/JF7Tlt/T9Wd7vsIuC4NvrmgcBBwKeAK4GD2midD6UbnOWilX9nkiRJ87O5pqRJ9ATgnNYv70eAC6rqo0k+D5yX5E3Ap4H3tu3fC7wvyQ5gF13SRlVdl+QC4PPAvcArWzNQkpwMXALsAZxVVdcN7+1JkiT1Z5InaeJU1WeBn5ql/Aa6kTFnlv8r8Ct9jvVm4M2zlF8MXLzsYCVJkgbM5pqSJEmSNEFM8iRJkiRpgpjkSZIkSdIEMcmTJEmSpAlikidJkiRJE8QkT5IkSZImiEmeJEmSJE0QkzxJkiRJmiAmeZIkSZI0QUzyJEmSJGmCmORJkiRJ0gQxyZMkSZKkCWKSJ0mSJEkTZN4kL8lZSW5Pcm1P2b5JLk1yfft3n1aeJO9IsiPJZ5Mc2rPP1rb99Um29pQfluRzbZ93JMmg36QkSZIkrRULuZN3NrBlRtmpwCeq6iDgE+05wLOBg9rjJOBd0CWFwGnAEcDhwGnTiWHb5uU9+818LUmSJEnSAs2b5FXVJ4FdM4qPBc5py+cAz+spP7c6lwN7J3kCcDRwaVXtqqo7gUuBLW3do6vq8qoq4NyeY0mSJEmSFmnPJe63rqpubctfA9a15f2Bm3u2u6WVzVV+yyzls0pyEt0dQtatW8fU1NQSw19Zu3fvHtvYwPiWa9Lj27ZtW9914/y+JUmS1FlqknefqqokNYhgFvBaZwJnAmzcuLE2bdo0jJddtKmpKcY1NjC+5Zr0+DZv3tx3XXfDXZIkSeNsqaNr3taaWtL+vb2V7wQO6NlufSubq3z9LOWSJEmSpCVYapJ3ETA9QuZW4MKe8hPaKJtHAne1Zp2XAEcl2acNuHIUcElbd3eSI9uomif0HEuSJEmStEgLmULhg8D/Bn4iyS1JTgTeAvxCkuuBn2/PAS4GbgB2AO8BXgFQVbuA04Er2+ONrYy2zV+1fb4MfGwwb03SWpXkgCSXJfl8kuuS/HYrd/oXSZI08ebtk1dVx/dZ9axZti3glX2OcxZw1izlVwGHzBeHJC3CvcDvVdXVSR4FbE9yKfASuulf3pLkVLrpX17NA6d/OYJuapcjeqZ/2QhUO85FbZTg6elfrqC7wLUFL1JJkqQxsNTmmpI0tqrq1qq6ui1/C/gC3ci9Tv8iSZIm3rJH15SkcZZkA/BTdHfchj79y1Knflm/fn3f6SzGaSqLcZ9SZJpxDt5qiXW1xClJg2SSJ2liJXkk8DfAq6rq7t5uc8Oa/mWpU7+cccYZnHLKKf2OOajwlm3cpxSZZpyDt1piXS1xStIg2VxTYyHJfY/t27c/4Lm0FEkeQpfgvb+q/rYVO/2LJEmaeCZ5kiZOG+nyvcAXqupPe1Y5/YskSZp4NteUNIl+Bngx8Lkk17Sy19JN93JBmwrmJuAFbd3FwDF0U7ncA7wUuulfkkxP/wIPnv7lbOARdKNqOrKmJEkaCyZ5kiZOVf0T0K+tr9O/SJKkiWZzTUmSJEmaIN7Jk8bYXAPPjNMIi5IkSRof3smTJEmSpAlikidJkiRJE8QkT5IkSZImiEmeJEmSJE0QkzxJkiRJmiAmeZIkSZI0QUzyJEmSJGmCmORJkiRJ0gQxyZMkSZKkCWKSJ0mSJEkTxCRPkiRJkiaISZ4kSZIkTRCTPEmSJEmaICZ5kiRJkjRBlpXkJbkxyeeSXJPkqla2b5JLk1zf/t2nlSfJO5LsSPLZJIf2HGdr2/76JFuX95YkSZIkae0axJ28zVX1jKra2J6fCnyiqg4CPtGeAzwbOKg9TgLeBV1SCJwGHAEcDpw2nRhKkiRJkhZnJZprHguc05bPAZ7XU35udS4H9k7yBOBo4NKq2lVVdwKXAltWIC5JkiRJmnh7LnP/Aj6epIC/rKozgXVVdWtb/zVgXVveH7i5Z99bWlm/8gdJchLdXUDWrVvH1NTUMsNfGbt37x7b2GA849u2bdt9y+vXr3/A83GLdZjnr/c8zNQvhuXGt5TXlCRJ0vhYbpL3zKrameRxwKVJvti7sqqqJYAD0ZLIMwE2btxYmzZtGtShB2pqaopxjQ3GM77Nmzfft7xt2zZOOeWU+55XDewrNBDDPH+952WmfudlufEt5TXHUZKzgOcAt1fVIa1sX+B8YANwI/CCqrozSYC3A8cA9wAvqaqr2z5bgT9sh31TVZ3Tyg8DzgYeAVwM/HatphMkSZIm1rKaa1bVzvbv7cCH6frU3daaYdL+vb1tvhM4oGf39a2sX7kkLcfZPLjp9yD7DL8LeHnPfjYzlyRJY2HJSV6SvZI8anoZOAq4FrgImB4hcytwYVu+CDihjbJ5JHBXa9Z5CXBUkn3aj6ejWpkkLVlVfRLYNaN4IH2G27pHV9Xl7e7duT3HkiRJGqnlNNdcB3y4a+XEnsAHquofklwJXJDkROAm4AVt+4vpmkLtoGsO9VKAqtqV5HTgyrbdG6tq5g8zSRqEQfUZ3r8tzyx/kKX2JZ7ZN7XXOPWNHMc+vrMxzsFbLbGuljglaZCWnORV1Q3A02cpvwN41izlBbyyz7HOAs5aaiyStFiD7jM8x+ssqS/xGWec8YC+qTOOOajwlm0c+/jOxjgHb7XEulrilKRBWokpFCRpXA2qz/DOtjyzXJIkaeRM8iStJQPpM9zW3Z3kyDYy5wk9x5IkSRqp5U6hIEljKckHgU3AfkluoRsl8y0Mrs/wK7h/CoWPtYckSdLImeRJq1Qb9OhBtm3bZv8ToKqO77NqIH2Gq+oq4JDlxChJkrQSbK4pSZIkSRPEJE+SJEmSJohJniRJkiRNEJM8SZIkSZogJnmSJEmSNEFM8iRJkiRpgpjkSZIkSdIEMcmTJEmSpAlikidJkiRJE8QkT5IkrWpJ+j4kaS0yyZMkSZKkCWKSJ0mSJEkTZM9RB6DVZ67mL1U1xEgkSZIkzeSdPEmSJEmaICZ5kiRJkjRBbK45RmwGKUmSJGm5vJMnSZIkSRPEJE+SJEmSJojNNZfAZpWSJEmSxtXEJ3njlJDNFYskSZIkDcLYNNdMsiXJl5LsSHLqqOORpPlYb0mSpHE0Fklekj2AdwLPBg4Gjk9y8GijkqT+rLckSdK4GoskDzgc2FFVN1TV94DzgGNHHJMkzcV6S5IkjaWMw0AhSZ4PbKmql7XnLwaOqKqTZ2x3EnBSe/oTwJeGGujC7Qd8Y9RBzMH4lsf45vfkqnrsiGNYUUOot8bhc1wI4xys1RInrJ5YFxrnxNdbktaOVTXwSlWdCZw56jjmk+Sqqto46jj6Mb7lMT4txlLrrdXyORrnYK2WOGH1xLpa4pSkQRqX5po7gQN6nq9vZZI0rqy3JEnSWBqXJO9K4KAkByZ5KHAccNGIY5KkuVhvSZKksTQWzTWr6t4kJwOXAHsAZ1XVdSMOaznGvUmp8S2P8WkY9dZq+RyNc7BWS5ywemJdLXFK0sCMxcArkiRJkqTBGJfmmpIkSZKkATDJkyRJkqQJYpK3CEluTPK5JNckuaqV7Zvk0iTXt3/3aeVJ8o4kO5J8NsmhPcfZ2ra/PsnWEcS2KcldbdtrkvxRz3G2JPlSi/vUQcQ2R3y/kuS6JD9MsnHG9q9pMXwpydHjFF+SDUm+03P+3t2z7rB2nB3t888KxvcnSb7Yvl8fTrJ3z/ZDPX9amvk+jyQPS3J+W39Fkg3Dj3JBcf5uks+37+Inkjx5FHG2WBb0HU/yH5PUzLpnWBYSZ5IXtPN6XZIPDDvGFsN8n/2TklyW5NPt8z9mRHGeleT2JNf2Wd/3b7IkTaSq8rHAB3AjsN+Msj8GTm3LpwJvbcvHAB8DAhwJXNHK9wVuaP/u05b3GXJsm4CPznKMPYAvAz8GPBT4DHDwCp67n6SbHHoK2NhTfnB77YcBB7aY9hij+DYA1/Y5zqfa5532+T97BeM7CtizLb+15/Md+vnzsaTPdN7PA3gF8O62fBxw/pjGuRn40bb8m6OIc6Gxtu0eBXwSuLz3//Y4xQkcBHya9vcBeNyYxnkm8Jtt+WDgxhF99v8eOHSOunnWv8k+fPjwMakP7+Qt37HAOW35HOB5PeXnVudyYO8kTwCOBi6tql1VdSdwKbBlyLH1cziwo6puqKrvAee1Y6yIqvpCVX1pllXHAudV1Xer6ivAjhbbuMQ3q/b5PrqqLq+qAs5l/nO+nPg+XlX3tqeX083TBmNy/jSvhXwevf+HPwQ8a1B3hxdh3jir6rKquqc97f0uDttCv+On010Y+ddhBtdjIXG+HHhn+ztBVd0+5BhhYXEW8Oi2/G+Arw4xvvuDqPoksGuOTfr9TZakiWSStzgFfDzJ9iQntbJ1VXVrW/4asK4t7w/c3LPvLa2sX/kwYwP46SSfSfKxJE+bJ+ZBmC2+foZ97hYbH8CBrXnS/0zys61s/xbTKOL7Nbqr1NNxDPv8afEW8nnct01L6O8CHjOU6GaJoZnve3Mi938Xh23eWFszvQOq6u+HGdgMCzmnTwWemuSfk1yeZKUuBs5lIXG+HnhRkluAi4H/PJzQFs36T9KaMhbz5K0iz6yqnUkeB1ya5Iu9K6uqkoxqTorFxHY18OSq2t36T3yErmnQUONrV17HxWLiuxV4UlXdkeQw4CM9ifLQ40vyOuBe4P0rHIM0pyQvAjYC/8+oY5lNkh8B/hR4yYhDWYg96erlTXR3Rj+Z5N9W1TdHGtWDHQ+cXVVnJPlp4H1JDqmqH446MElay7yTtwhVtbP9ezvwYbqmLLdNN/lo/043qdkJHNCz+/pW1q98aLFV1d1VtbstXww8JMl+KxXbHPH1M9Rzt9j4WjPIO9rydro+K09tsfQ2U1vx+JK8BHgO8MLWRBRGcP60JAv5PO7bJsmedM3h7hhKdLPE0Mz6vUny88DrgOdW1XeHFNtM88X6KOAQYCrJjXR9sy4aweArCzmntwAXVdX3W7Pr/8PKX4ybaSFxnghcAFBV/xt4OLDfUKJbHOs/SWuKSd4CJdkryaOml+kGvbgWuAiYHiFzK3BhW74IOKGN6HUkcFdrOnkJcFSSfdKNdnlUKxtabEkeP92vJ8nhdN+DO4ArgYOSHJjkoXQDPVy0nNjmia+fi4Dj0o0seCDdD5tPjUt8SR6bZI+2/GMtvhva53t3kiPb+T2B+78PA4+vNd/6A7of1ff07DLU86clW8jn0ft/+PnAP/Yk88Myb5xJfgr4S7rv4ij6jk2bM9aququq9quqDVW1ga7/4HOr6qpxirP5CN1dPNpFuKfSDdQ1TAuJ81+AZwEk+Um6JO/rQ41yYfr9TZakiWRzzYVbB3y45UZ7Ah+oqn9IciVwQZITgZuAF7TtL6YbzWsHcA/wUoCq2pXkdLo/ngBvrKq5OouvRGzPB34zyb3Ad4Dj2g/He5OcTJd07gGcVVXXLTO2ueL7JeC/Ao8F/j7JNVV1dFVdl+QC4PN0zRBfWVU/ABiH+OhGcXtjku8DPwR+o+czfAVwNvAIun5Jg+ib1C++HXQjaF7a1l1eVb8xgvOnJaiqWf+/JXkjcFVVXQS8l6752w66QSWOG9M4/wR4JPDf23fxX6rquWMa68gtMM7pC4KfB34A/P50C4Ixi/P3gPck+R26vsMvGcGFCJJ8kC4p3i9d/8DTgIe09/Fu+vxNlqRJlRHUxZIkSZKkFWJzTUmSJEmaICZ5kiRJkjRBTPIkSZIkaYKY5EmSJEnSBDHJkyRJkqQJYpInSZIkSRPEJE+SJEmSJsj/D1Tl4pMKYCTHAAAAAElFTkSuQmCC\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "df.hist(color = \"k\",\n",
        "        bins = 30,\n",
        "        figsize = (15, 10))\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "gb57x-rPe5mb"
      },
      "source": [
        "A visual analysis of the histograms presented allows us to make preliminary assumptions about the variability of the source data.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "-hQDR1PGFVIK"
      },
      "source": [
        "Now we will use Box Plot. It will allow us to compactly visualize the main characteristics of the feature distribution (the median, lower and upper quartile, minimal and maximum, outliers).\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "9lAwux3g4Q6C",
        "scrolled": true,
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 420
        },
        "outputId": "f02a819e-ce06-4d5b-9058-c6f27d087f66"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 576x432 with 1 Axes>"
            ],
            "image/png": "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\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "df.boxplot(column = \"age\",\n",
        "           by = \"marital\")\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "2Ci3YxUBgDjB"
      },
      "source": [
        "The plot shows that unmarried people are on average younger than divorced and married ones. For the last two groups, there is an outlier zone over 70 years old, and for unmarried - over 50.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "yQ5td0XaFVIL"
      },
      "source": [
        "**Now we will try to do this by data grouping on other features:**"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "wtnHOQ3sFVIM",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 1000
        },
        "outputId": "9b257437-55e5-4307-b6ad-505d768df207"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 1440x1440 with 1 Axes>"
            ],
            "image/png": "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5EgOHDiQffv2paurK/v27cuBAwdy5MiR2qXBinv44Yezd+/e3Hfffenu7s59992XvXv35uGHH65d2oYwNjaWiYmJtFqtdHR0pNVqZWJiImNjY7VLgxXn+gcAWJ8EVEs0NzeX4eHhRWPDw8OZm5urVBGsnqZpcu+99y4au/fee9M0TaWKNpbZ2dn09/cvGuvv78/s7GylimD1uP4BANYnAdUSdXZ2Znx8fNHY+Ph4Ojs7K1UEq6eUkrvvvnvR2N13351SSqWKNpaenp7MzMwsGpuZmUlPT0+limD1uP4BANYna1At0Z49ey6tOXXzzTfn4MGD2b9//9fMqoL16Pbbb8/hw4eTJHfeeWfuuuuuHD58OHfccUflyjaG0dHRDA0NXVqDZ3p6OkNDQ25xYkNw/QMArE8CqiVaWAj9nnvuydzcXDo7OzM8PGyBdDaEY8eOZWBgIOPj4zl8+HBKKbnjjjsskL5KFhaCHhkZyezsbHp6ejI2NmaBaDYE1z8AwPokoFqGQ4cO5dChQzl+/Hh27NhRuxxYVQthlOu/jsHBwQwODuo/G5LrHwBg/bEGFQAAAABVCagAAAAAqEpABQAAAEBVAioAAAAAqhJQLcPAwEA2bdqUVquVTZs2ZWBgoHZJsGr6+vpSSkmr1UopJX19fbVL2lC8/7CRdXd3L3r/6e7url0SAADLJKBaooGBgTz00EMZHh7Oxz72sQwPD+ehhx7yRyIbQl9fX06dOpVdu3blox/9aHbt2pVTp04JqVaJ9x82su7u7jz//PPZtm1bPvShD2Xbtm15/vnnhVQAAGucgGqJHn744ezduzf33Xdfuru7c99992Xv3r15+OGHa5cGK24hnDp69GiuvfbaHD169FJIxcrz/sNGthBOPfnkk3njG9+YJ5988lJIBQDA2iWgWqKmaXLvvfcuGrv33nvTNE2limB1TUxMXHGbleP9h43uE5/4xBW3AQBYewRUS1RKyd13371o7O67704ppVJFsLqGhoauuM3K8f7DRvfWt771itsAAKw9Aqoluv3223P48OHcddddOXv2bO66664cPnw4t99+e+3SYMVt3749U1NT2b17d5577rns3r07U1NT2b59e+3SNgTvP2xk11xzTU6fPp03velN+dznPpc3velNOX36dK655prapQEAsAwdtQtYq44dO5aBgYGMj4/n8OHD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\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "df.boxplot(column = \"age\",\n",
        "           by = [\"marital\", \"housing\"],\n",
        "           figsize = (20, 20))\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "MZB02pxKhReu"
      },
      "source": [
        "As we can see, age and marital status do not have any significant influence on having a housing loan.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "VUMjKczqTThq"
      },
      "source": [
        "\n",
        "## Tasks\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "jLCT0HXkTThr"
      },
      "source": [
        "In this section, we will solve some tasks with the source bank dataset.\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "q7C0DMPdTThs"
      },
      "source": [
        "### Question 1\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "psvWjxS4TThs"
      },
      "source": [
        "List of 10 clients with the largest number of contacts.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "unSAHwIPTTht",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 474
        },
        "outputId": "39eeb23b-25e3-4fde-ca05-cbc9a4fc7d53"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "       age            job  marital            education  default  housing  \\\n",
              "4107    32         admin.  married    university.degree  unknown  unknown   \n",
              "18728   54         admin.  married    university.degree  unknown      yes   \n",
              "13447   32     technician   single    university.degree       no      yes   \n",
              "4168    29     technician  married  professional.course       no      yes   \n",
              "5304    44        retired  married             basic.9y       no      yes   \n",
              "11033   38    blue-collar  married             basic.4y       no      yes   \n",
              "18754   36         admin.   single    university.degree       no       no   \n",
              "11769   56  self-employed  married  professional.course       no       no   \n",
              "4114    52   entrepreneur  married    university.degree       no       no   \n",
              "11593   43     technician  married          high.school       no      yes   \n",
              "\n",
              "          loan    contact month day_of_week  ...  campaign  pdays  previous  \\\n",
              "4107   unknown  telephone   may         mon  ...        56    999         0   \n",
              "18728       no   cellular   jul         thu  ...        43    999         0   \n",
              "13447      yes  telephone   jul         wed  ...        43    999         0   \n",
              "4168        no  telephone   may         mon  ...        42    999         0   \n",
              "5304        no  telephone   may         fri  ...        42    999         0   \n",
              "11033       no  telephone   jun         wed  ...        41    999         0   \n",
              "18754       no   cellular   jul         thu  ...        40    999         0   \n",
              "11769      yes  telephone   jun         fri  ...        40    999         0   \n",
              "4114        no  telephone   may         mon  ...        39    999         0   \n",
              "11593       no  telephone   jun         fri  ...        37    999         0   \n",
              "\n",
              "          poutcome emp.var.rate  cons.price.idx  cons.conf.idx  euribor3m  \\\n",
              "4107   nonexistent         1.10           93.99         -36.40       4.86   \n",
              "18728  nonexistent         1.40           93.92         -42.70       4.97   \n",
              "13447  nonexistent         1.40           93.92         -42.70       4.96   \n",
              "4168   nonexistent         1.10           93.99         -36.40       4.86   \n",
              "5304   nonexistent         1.10           93.99         -36.40       4.86   \n",
              "11033  nonexistent         1.40           94.47         -41.80       4.96   \n",
              "18754  nonexistent         1.40           93.92         -42.70       4.97   \n",
              "11769  nonexistent         1.40           94.47         -41.80       4.96   \n",
              "4114   nonexistent         1.10           93.99         -36.40       4.86   \n",
              "11593  nonexistent         1.40           94.47         -41.80       4.96   \n",
              "\n",
              "       nr.employed  y  \n",
              "4107       5191.00  0  \n",
              "18728      5228.10  0  \n",
              "13447      5228.10  0  \n",
              "4168       5191.00  0  \n",
              "5304       5191.00  0  \n",
              "11033      5228.10  0  \n",
              "18754      5228.10  0  \n",
              "11769      5228.10  0  \n",
              "4114       5191.00  0  \n",
              "11593      5228.10  0  \n",
              "\n",
              "[10 rows x 21 columns]"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-0d78999e-89f6-4a34-a740-ebe7b9e22e7d\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
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
              "      <th>age</th>\n",
              "      <th>job</th>\n",
              "      <th>marital</th>\n",
              "      <th>education</th>\n",
              "      <th>default</th>\n",
              "      <th>housing</th>\n",
              "      <th>loan</th>\n",
              "      <th>contact</th>\n",
              "      <th>month</th>\n",
              "      <th>day_of_week</th>\n",
              "      <th>...</th>\n",
              "      <th>campaign</th>\n",
              "      <th>pdays</th>\n",
              "      <th>previous</th>\n",
              "      <th>poutcome</th>\n",
              "      <th>emp.var.rate</th>\n",
              "      <th>cons.price.idx</th>\n",
              "      <th>cons.conf.idx</th>\n",
              "      <th>euribor3m</th>\n",
              "      <th>nr.employed</th>\n",
              "      <th>y</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>4107</th>\n",
              "      <td>32</td>\n",
              "      <td>admin.</td>\n",
              "      <td>married</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>unknown</td>\n",
              "      <td>unknown</td>\n",
              "      <td>unknown</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>56</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>18728</th>\n",
              "      <td>54</td>\n",
              "      <td>admin.</td>\n",
              "      <td>married</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>unknown</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>jul</td>\n",
              "      <td>thu</td>\n",
              "      <td>...</td>\n",
              "      <td>43</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.92</td>\n",
              "      <td>-42.70</td>\n",
              "      <td>4.97</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>13447</th>\n",
              "      <td>32</td>\n",
              "      <td>technician</td>\n",
              "      <td>single</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>yes</td>\n",
              "      <td>telephone</td>\n",
              "      <td>jul</td>\n",
              "      <td>wed</td>\n",
              "      <td>...</td>\n",
              "      <td>43</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.92</td>\n",
              "      <td>-42.70</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4168</th>\n",
              "      <td>29</td>\n",
              "      <td>technician</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>42</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5304</th>\n",
              "      <td>44</td>\n",
              "      <td>retired</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.9y</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>42</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>11033</th>\n",
              "      <td>38</td>\n",
              "      <td>blue-collar</td>\n",
              "      <td>married</td>\n",
              "      <td>basic.4y</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>jun</td>\n",
              "      <td>wed</td>\n",
              "      <td>...</td>\n",
              "      <td>41</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>94.47</td>\n",
              "      <td>-41.80</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>18754</th>\n",
              "      <td>36</td>\n",
              "      <td>admin.</td>\n",
              "      <td>single</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>cellular</td>\n",
              "      <td>jul</td>\n",
              "      <td>thu</td>\n",
              "      <td>...</td>\n",
              "      <td>40</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>93.92</td>\n",
              "      <td>-42.70</td>\n",
              "      <td>4.97</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>11769</th>\n",
              "      <td>56</td>\n",
              "      <td>self-employed</td>\n",
              "      <td>married</td>\n",
              "      <td>professional.course</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>telephone</td>\n",
              "      <td>jun</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>40</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>94.47</td>\n",
              "      <td>-41.80</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4114</th>\n",
              "      <td>52</td>\n",
              "      <td>entrepreneur</td>\n",
              "      <td>married</td>\n",
              "      <td>university.degree</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>may</td>\n",
              "      <td>mon</td>\n",
              "      <td>...</td>\n",
              "      <td>39</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.10</td>\n",
              "      <td>93.99</td>\n",
              "      <td>-36.40</td>\n",
              "      <td>4.86</td>\n",
              "      <td>5191.00</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>11593</th>\n",
              "      <td>43</td>\n",
              "      <td>technician</td>\n",
              "      <td>married</td>\n",
              "      <td>high.school</td>\n",
              "      <td>no</td>\n",
              "      <td>yes</td>\n",
              "      <td>no</td>\n",
              "      <td>telephone</td>\n",
              "      <td>jun</td>\n",
              "      <td>fri</td>\n",
              "      <td>...</td>\n",
              "      <td>37</td>\n",
              "      <td>999</td>\n",
              "      <td>0</td>\n",
              "      <td>nonexistent</td>\n",
              "      <td>1.40</td>\n",
              "      <td>94.47</td>\n",
              "      <td>-41.80</td>\n",
              "      <td>4.96</td>\n",
              "      <td>5228.10</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>10 rows × 21 columns</p>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-0d78999e-89f6-4a34-a740-ebe7b9e22e7d')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-0d78999e-89f6-4a34-a740-ebe7b9e22e7d button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-0d78999e-89f6-4a34-a740-ebe7b9e22e7d');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 32
        }
      ],
      "source": [
        "df.sort_values(by = \"campaign\", ascending = False).head(10)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "xwaZlbEbTThu"
      },
      "source": [
        "### Question 2\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "_PNycuTMTThv"
      },
      "source": [
        "Determine the median age and the number of contacts for different levels of client education.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 9,
      "metadata": {
        "id": "o2Hxx2FzTThw",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 363
        },
        "outputId": "13708268-e3b8-49aa-f656-7d06e549ee98"
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "                     mean           count         \n",
              "                      age campaign    age campaign\n",
              "education                                         \n",
              "basic.4y            47.60     2.60   4176     4176\n",
              "basic.6y            40.45     2.56   2292     2292\n",
              "basic.9y            39.06     2.53   6045     6045\n",
              "high.school         38.00     2.57   9515     9515\n",
              "illiterate          48.50     2.28     18       18\n",
              "professional.course 40.08     2.59   5243     5243\n",
              "university.degree   38.88     2.56  12168    12168\n",
              "unknown             43.48     2.60   1731     1731"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-d706dc8f-31b3-46fa-b874-163e61616294\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead tr th {\n",
              "        text-align: left;\n",
              "    }\n",
              "\n",
              "    .dataframe thead tr:last-of-type th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr>\n",
              "      <th></th>\n",
              "      <th colspan=\"2\" halign=\"left\">mean</th>\n",
              "      <th colspan=\"2\" halign=\"left\">count</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th></th>\n",
              "      <th>age</th>\n",
              "      <th>campaign</th>\n",
              "      <th>age</th>\n",
              "      <th>campaign</th>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>education</th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "      <th></th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>basic.4y</th>\n",
              "      <td>47.60</td>\n",
              "      <td>2.60</td>\n",
              "      <td>4176</td>\n",
              "      <td>4176</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>basic.6y</th>\n",
              "      <td>40.45</td>\n",
              "      <td>2.56</td>\n",
              "      <td>2292</td>\n",
              "      <td>2292</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>basic.9y</th>\n",
              "      <td>39.06</td>\n",
              "      <td>2.53</td>\n",
              "      <td>6045</td>\n",
              "      <td>6045</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>high.school</th>\n",
              "      <td>38.00</td>\n",
              "      <td>2.57</td>\n",
              "      <td>9515</td>\n",
              "      <td>9515</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>illiterate</th>\n",
              "      <td>48.50</td>\n",
              "      <td>2.28</td>\n",
              "      <td>18</td>\n",
              "      <td>18</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>professional.course</th>\n",
              "      <td>40.08</td>\n",
              "      <td>2.59</td>\n",
              "      <td>5243</td>\n",
              "      <td>5243</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>university.degree</th>\n",
              "      <td>38.88</td>\n",
              "      <td>2.56</td>\n",
              "      <td>12168</td>\n",
              "      <td>12168</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>unknown</th>\n",
              "      <td>43.48</td>\n",
              "      <td>2.60</td>\n",
              "      <td>1731</td>\n",
              "      <td>1731</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-d706dc8f-31b3-46fa-b874-163e61616294')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-d706dc8f-31b3-46fa-b874-163e61616294 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-d706dc8f-31b3-46fa-b874-163e61616294');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 9
        }
      ],
      "source": [
        "df.pivot_table(\n",
        "    [\"age\", \"campaign\"],\n",
        "    [\"education\"],\n",
        "    aggfunc = [\"mean\", \"count\"],\n",
        ")\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Fs2Wf3RQTThw"
      },
      "source": [
        "### Question 3\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "QPr0VwEXTThw"
      },
      "source": [
        "Output box plot to analyze the client age distribution by their education level.\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "YO648QDYTThy",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 958
        },
        "outputId": "5d86512b-3429-4138-da41-5297ff1e86f1"
      },
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 1080x1080 with 1 Axes>"
            ],
            "image/png": "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JUuWHPpOMA0EROY0A68PFvUaLPPmzcuzzz6bhQsX5qqrrsrChQvz7LPPCokwCRYuXJinnnoqy5Ytyyc+8YksW7YsTz31lJA4Qy1ZsiQ7duzI6aefng0bNuT000/Pjh07hERmJAGROc3A64NFvQbLaDh88skn87KXvSxPPvnknpAITMxoOHzggQfy4he/OA888MCekMjMMxoON2/enJNOOimbN2/eExJhphEQmdO2bt2ac845Z69555xzTrZu3TpNPeJg1Gvw3HnnnQedBo7cpz/96YNOM7PcfPPNB52GmUJAZE5bvnx57rrrrr3m3XXXXVm+fPk09YiDUa/B8+pXv/qg08CRe+1rX3vQaWaWCy644KDTMFMIiMxpBl4fLOo1WI466qiMjIxk0aJF+frXv55FixZlZGQkRx3lrQcm6thjj822bdty6qmn5jvf+U5OPfXUbNu2N42RNQAAIABJREFULccee+x0d41xLF68OFu2bMmKFSvy8MMPZ8WKFdmyZUsWL1483V2D/UxomAsYdAZeHyzqNVh2796defPmZWRkJJdddlmSXmjcvXv3NPcMBt/IyEgWLlyYbdu25S1veUuSXmgcGRmZ5p4xnu3bt2fJkiXZsmXLnvesxYsXZ/v27dPcM9ifr3GZ8wy8PljUa7Ds3r17r4GhhUOYPCMjI3utX8LhzLZ9+/a96iUcMlMJiAAAACQREIEBs2HDhqxYsSLnnntuVqxYYQzEGe7oo4/ea2Doo48+erq7BDAtFixYsNf2cMGCBdPdJRiXgAgMjA0bNmTt2rW58sorc+utt+bKK6/M2rVrhcQZ6uijj873vve9LF26NB/72MeydOnSfO973xMSgTlnwYIF2bVrV0444YR89KMfzQknnJBdu3YJicxIAiIwMNatW5f169dn1apVmT9/flatWpX169dn3bp10901xjEaDh9++OEsW7YsDz/88J6QCDCXjIbDHTt25LTTTsuOHTv2hESYaZzFFBgYW7duzTnnnLPXvHPOOSdbt26dph5xKMPDw/tNG7cSDqyq+tpea62v7c1ld955537Tr3jFK6apN3Bg9iACA2P58uW566679pp31113CRwz2NDQ0EGngb211p7330vec+MR3U847K9Xv/rVB52GmUJABAbG2rVrs3r16mzcuDG7du3Kxo0bs3r16qxdu3a6u8Y4XvCCF+SRRx7JSSedlG3btuWkk07KI488khe84AXT3TWAvpo/f34ee+yxLF68OPfff38WL16cxx57LPPnO5iPmcerEhgYo2MeXn755dm6dWuWL1+edevWGQtxhnrmmWdy9NFH55FHHsnb3va2JL3Q+Mwzz0xzzwD6a+fOnVmwYEEee+yxvP3tb0/SC407d+6c5p7B/uxBBAbKxRdfnM2bN+eOO+7I5s2bhcMZ7plnntlrYGjhEJirdu7cudf2UDhkphIQAQAASCIggoHXAYApd8opp6SqsmrVqlRVTjnllOnuEozLbxCZ00YHXl+/fn12796defPmZfXq1Uni0EUAYFKccsopeeihh3LWWWfl3e9+dz784Q9n06ZNOeWUU/Lggw9Od/dgL/YgMqcZeB0AmGqj4fDuu+/OiSeemLvvvjtnnXVWHnrooenuGuxHQGROM/A6ANAPn/rUpw46DTOFgMicZuB1AKAf3vjGNx50GmYKAZE5zcDrAMBUO/nkk7Np06acffbZefTRR3P22Wdn06ZNOfnkk6e7a7AfJ6lhTjPwOgAw1R588MGccsop2bRpUzZt2pSkFxqdoIaZyB5E5jwDrwMAU+3BBx9May0bN25Ma004ZMYSEAEAAEgiIAIAANDxG0TmvPPPPz+33357Wmupqrzuda/LrbfeOt3dgllhyZIl2bFjx57pxYsXZ/v27dPYI4DpsXDhwjz11FN7po899tiMjIxMY49gfPYgMqedf/75ue222/KOd7wjf/Inf5J3vOMdue2223L++edPd9dg4I2Gw9NPPz0bNmzI6aefnh07dmTJkiXT3TWAvhoNh8uWLcsnPvGJLFu2LE899VQWLlw43V2D/QiIzGm33357LrvssnzkIx/JwoUL85GPfCSXXXZZbr/99unuGgy80XC4efPmnHTSSdm8efOekAgwl4yGwwceeCAvfvGL88ADD+wJiTDTCIjMaa21fPCDH9xr3gc/+MG01qapR3NTVT3vv1WrVh3R/apquh/unHLzzTcfdBpgrvj0pz990GmYKQRE5rSqynvf+9695r33ve8VIvqstfa8/17ynhuP6H7Cf39dcMEFB50GmCte+9rXHnQaZgoBkTntda97Xa666qq8853vzMjISN75znfmqquuyute97rp7hoMvMWLF2fLli1ZsWJFHn744axYsSJbtmzJ4sWLp7trAH117LHHZtu2bTn11FPzne98J6eeemq2bduWY489drq7BvtxFlPmtFtvvTXnn39+fvM3fzNXXXVVqirnnXees5jCJNi+fXuWLFmSLVu25OKLL07iLKbA3DQyMpKFCxdm27Ztectb3pLEWUyZuexBZM679dZb8+yzz2bjxo159tlnhUOYRNu3b09rLRs3bkxrTTgE5qyRkZG9tofCITOVgAgAAEASARGyYcOGrFixIueee25WrFiRDRs2THeXYNZYsmTJXmedNQYiMFfNmzdvr+3hvHnzprtLMC4BkTltw4YNWbt2ba688srceuutufLKK7N27VohESbBkiVL9oyFuGHDhj1jIAqJwFwzb968PPvss1m4cGGuuuqqLFy4MM8++6yQyIwkIDKnrVu3LuvXr8+qVasyf/78rFq1KuvXr8+6deumu2sw8EbD4ebNm3PSSSdl8+bNe0IiwFwyGg6ffPLJvOxlL8uTTz65JyTCTCMgMqdt3bo155xzzl7zzjnnnGzdunWaegSzy80333zQaYC54s477zzoNMwUAiJz2vLly3PXXXftNe+uu+7K8uXLp6lHMLtccMEFB50GmCte/epXH3QaZgoBkTlt7dq1Wb16dTZu3Jhdu3Zl48aNWb16ddauXTvdXYOBt3jx4mzZsiUrVqzIww8/nBUrVmTLli1ZvHjxdHcNoK+OOuqojIyMZNGiRfn617+eRYsWZWRkJEcd5aM4M8/86e4ATKfRwbsvv/zybN26NcuXL8+6dev2zAeO3Pbt27NkyZJs2bJlzzq1ePFiYyECc87u3bszb968jIyM5LLLLkvSC427d++e5p7B/nxtwZx38cUXZ/PmzbnjjjuyefNm4RAm0fbt2/caGFo4BOaq3bt377U9FA6ZqQREAAAAkjjEFIAptGDBguzatWvP9Pz587Nz585p7BEAcDD2IAIwJUbD4QknnJCPfvSjOeGEE7Jr164sWLBgursGAByAgAjAlBgNhzt27Mhpp52WHTt27AmJAMDM5BBTZqWq6mt7rbW+tgeDYryBoV/xildMU28AJpfPG8xG9iAyK7XWnvffS95z4xHdz8YaDszA0MBs5vMGs5GACMCUmD9/fh577LEsXrw4999/fxYvXpzHHnss8+c7eAUAZirv0gBMiZ07d2bBggV57LHH8va3vz2Js5gCwExnDyIAU2bnzp17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\n"
          },
          "metadata": {
            "needs_background": "light"
          }
        }
      ],
      "source": [
        "df.boxplot(column = \"age\",\n",
        "  by = \"education\",\n",
        "  figsize = (15, 15))\n",
        "plt.show()"
      ]
    }
  ],
  "metadata": {
    "colab": {
      "collapsed_sections": [],
      "name": "Proj1_EDA_Pandas_Banking.ipynb",
      "provenance": []
    },
    "kernelspec": {
      "display_name": "Python",
      "language": "python",
      "name": "conda-env-python-py"
    },
    "language_info": {
      "codemirror_mode": {
        "name": "ipython",
        "version": 3
      },
      "file_extension": ".py",
      "mimetype": "text/x-python",
      "name": "python",
      "nbconvert_exporter": "python",
      "pygments_lexer": "ipython3",
      "version": "3.7.12"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 0
}
