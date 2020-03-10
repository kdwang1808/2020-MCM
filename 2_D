#!/usr/bin/env python
# -*- coding:utf-8 -*-

from __future__ import print_function
import seaborn as sns
from scipy import stats
import numpy as np
import statsmodels.api as sm
from statsmodels.graphics.api import qqplot
import matplotlib.pyplot as plt
import pandas as pd
from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()


sns.set_style("whitegrid")
lists = [[258, 269, 11, 88, 244], [13, 19, 0, 35, 40], [1131, 1793, 2633, 2067, 3725]]
hair = [258, 269, 11, 88, 244]
micro = [13, 19, 0, 35, 40]
baby = [1131, 1793, 2633, 2067, 3725]
filename = ['hair', 'micro', 'baby']
year = []
month = []
axis_x = []
for i in range(8):
    for j in range(12):
        if (j == 8) and (i == 7):
            break
        year.append(i + 2008)
        month.append(j + 1)
for i in range(92):
    axis_x.append(i * 1.0)


def get_data(df_argu):
    df_temp = df_argu
    # 获得数据 数据处理
    sold = []
    score = []
    #   vote = []
    temp = []
    for k in range(92):  # 12months*7years+8months
        sold.append(0)
        #        vote.append(0)
        score.append(0)
        temp.append(k)
    total_sold = 0
    # 年
    for k in range(8):
        df_temp2 = df_temp[df_temp['yy'] == (k + 2008)]
        # 月
        for month_cnt in range(12):
            if (k == 7) and (month_cnt >= 8):
                break
            cnt = 0
            df4 = df_temp2[df_temp2['mm'] == (month_cnt + 1)]
            for num in df4['star_rating']:
                score[k * 12 + month_cnt] += num
                cnt += 1
            #            for useful_votes in df4['helpful_votes']:
            #               vote[k * 12 + month_cnt] += useful_votes
            sold[k * 12 + month_cnt] = cnt
            total_sold += cnt
            if cnt != 0:
                # 取月平均评分
                score[k * 12 + month_cnt] = score[k * 12 + month_cnt] * 1.0 / cnt
                # 月平均得票数目
            #               vote[k * 12 + month_cnt] = vote[k * 12 + month_cnt] * 1.0 / cnt
            else:
                score[k * 12 + month_cnt] = 0.0
    #               vote[k * 12 + month_cnt] = 0.0
    #    ave_sold = total_sold * 1.0 / 92
    dates = pd.date_range('2008-01', '2015-09', freq='M')
    data1 = {'star_rating': score, 'sold': sold}
    df_temp = pd.DataFrame(data=data1, index=dates)
    #    df2.to_csv(name)
    return df_temp


#    df2 = df.diff()
#    plt.figure(figsize=(40, 20))
date = pd.date_range('2008-01', '2015-09', freq='M')
fig = plt.figure(figsize=(24, 24))

l1 = [1, 4, 7, 10, 13]
l2 = [2, 5, 8, 11, 14]
l3 = [3, 6, 9, 12, 15]
for i in range(5):
    # 获取正面信息
    name = 'hair'
    name1 = name + '_pos.csv'
    df = pd.read_csv(open(name1, encoding="utf-8"))
    df1 = df[df["product_parent"] == hair[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df3 = get_data(df2)
    # 获取负面信息
    name1 = name + '_neg.csv'
    df = pd.read_csv(open(name1, encoding="UTF-8"))
    df1 = df[df["product_parent"] == hair[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df4 = get_data(df2)
    # 显示

    df3_sold = pd.Series(df3['sold'], index=date)
    df4_sold = pd.Series(df4['sold'], index=date)
    df3_score = pd.Series(df3['star_rating'], index=date)
    df4_score = pd.Series(df4['star_rating'], index=date)
    plt.subplot(5, 3, l1[i])
    plt.plot(df3_sold.diff(), 'r', label='positive_comments', lw=1, linestyle='-')
    plt.plot(df3_score, 'g', label='positive_mean', lw=1)
    plt.plot(df4_sold.diff(), 'y', label='negative_comments', lw=1, linestyle='-')
    plt.plot(df4_score, 'b', label='negative_mean', lw=1)
    plt.title('Observation on product hair_dryer' + str(i + 1))
    plt.xlabel('year')
    plt.ylabel('Star rating mean & Numbers of comments')

for i in range(5):
    # 获取正面信息
    name = 'micro'
    name1 = name + '_pos.csv'
    df = pd.read_csv(open(name1, encoding="UTF-8"))
    df1 = df[df["product_parent"] == micro[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df3 = get_data(df2)
    # 获取负面信息
    name1 = name + '_neg.csv'
    df = pd.read_csv(open(name1, encoding="UTF-8"))
    df1 = df[df["product_parent"] == micro[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df4 = get_data(df2)
    # 显示

    df3_sold = pd.Series(df3['sold'], index=date)
    df4_sold = pd.Series(df4['sold'], index=date)
    df3_score = pd.Series(df3['star_rating'], index=date)
    df4_score = pd.Series(df4['star_rating'], index=date)
    plt.subplot(5, 3, l2[i])
    plt.plot(df3_sold.diff(), 'r', label='positive_comments', lw=1, linestyle='-')
    plt.plot(df3_score, 'g', label='positive_mean', lw=1)
    plt.plot(df4_sold.diff(), 'y', label='negative_comments', lw=1, linestyle='-')
    plt.plot(df4_score, 'b', label='negative_mean', lw=1)
    plt.title('Observation on product microwave' + str(i + 1))
    plt.xlabel('year')
    plt.ylabel('Star rating mean & Numbers of comments')

for i in range(5):
    # 获取正面信息
    name = 'baby'
    name1 = name + '_pos.csv'
    df = pd.read_csv(open(name1, encoding="UTF-8"))
    df1 = df[df["product_parent"] == baby[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df3 = get_data(df2)
    # 获取负面信息
    name1 = name + '_neg.csv'
    df = pd.read_csv(open(name1, encoding="UTF-8"))
    df1 = df[df["product_parent"] == baby[i]]
    df2 = pd.DataFrame(df1, columns=['yy', 'star_rating', 'mm'])
    df4 = get_data(df2)
    # 显示

    df3_sold = pd.Series(df3['sold'], index=date)
    df4_sold = pd.Series(df4['sold'], index=date)
    df3_score = pd.Series(df3['star_rating'], index=date)
    df4_score = pd.Series(df4['star_rating'], index=date)
    plt.subplot(5, 3, l3[i])
    plt.plot(df3_sold.diff(), 'r', label='positive_comments', lw=1, linestyle='-')
    plt.plot(df3_score, 'g', label='positive_mean', lw=1)
    plt.plot(df4_sold.diff(), 'y', label='negative_comments', lw=1, linestyle='-')
    plt.plot(df4_score, 'b', label='negative_mean', lw=1)
    plt.title('Observation on product baby_pacifier' + str(i + 1))
    plt.xlabel('year')
    plt.ylabel('Star rating mean & Numbers of comments')
# plt.show()
plt.savefig("2_D_diff_1")
