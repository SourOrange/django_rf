# django_rf
## django_rest_framework
不懂啊，之前看了文档，粗略看了，还是萌萌滴o(*￣︶￣*)o,这里建议多多学习，天天开心。
废话不多说，干掉拼多多，开始 给自己看的drf。
个人是重新建立一个虚拟环境的，毕竟听某人说新版本的又是坑，哎，真是让我这个新手望而生畏，以下是 根据 django 的一些命令教程过来的，
learndrf, 是我的虚拟环境。并且 django==1.11, pip install djangorestframework==3.7, 接着跟着官网的 quickstart 走了一遍，或者和
我fork 的那个 文档走一遍也行。不过建议两个都试试。后来在某人的教程中，说了 序列化和反序列化的操作，就是那个 serializers 的文件夹，里面
那个 MusicSerializer(), 因为我按照 另外一个教程 走了一遍，所以去 python manage.py shell,中调试 序列化，以后的代码也是一样的，
在我们传入 from ....... 引入俩东西以后， 实例化那个Music 类， mus1 = Music.objects.all()[0], 然后，我们可以把这个实例传入 序列化中，
也就是  ser1 = MusicSerializer(mus1), 并且可以读出数据， ser1.data, 会显示其中的数据，当然了，如果你全部直接传进去，可以这么写。
all_music = Music.objects.all(), all_ser = MusicSerializer(all_music, many=True), 注意了，必须加个 many 参数，你可以不加的，但是运行
all_ser.data 的时候会报错，所以记得加了 many 这个参数。。1111111，以上，是我们在原来的数据中读取的，那么我们在外面传入一个数据呢，就是反序列化了吧。
反的就需要通过俩点  .is_valid(), .validated_data, 验证是否符合，符合后的数据样子， 然后我们就可以传入了，例如你的models中原本传入了三个song,那么等下这个 soong， 会变成 4个，因为你从外面传了一个进来。具体做法就是这么莱迪，首先实例一个数据， mus_data = {'song': '窗外的阳光', 'singer': '小青'},
然后 传入序列 ser_mus_data = MusicSerializer(data=mus_data), 看到没，里面要传入一个data参数。然后再来验证， ser_mus_data.is_valid(), 会返回 True, ser_mus_data.validated_data, 会返回 OrderedDict([('song', '窗外的阳光'), ('singer', '小青')])， 接着我们要把这个添加到里面去的做法是，
music4 = Music(), music4.song = ser_mus_data['song'], music4.singer = ser_mus_data['singer'], music4.save(), 这样我们就创建完毕了，你可以通过 Music.objects.all(), 可以看到有第四个了。好了，先到这里。
