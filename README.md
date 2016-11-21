multi, err := bt.InitMulti("pict.tar.gz")
	if err != nil {
		fmt.Println(err)
	}
	partInfo, err := multi.PutPart("/home/qwg/pict.tar.gz", sdk.Private, 1024*1024*3)
	if err != nil {
		fmt.Println(err)
	}
	listPart, err := multi.ListPart()
	if err != nil {
		fmt.Println(err)
	}
	for k, v := range listPart {
		if partInfo[k].ETag != v.ETag {
			fmt.Println("分片不匹配")
		}
	}
	err = multi.Complete(partInfo)
	if err != nil {
		fmt.Println(err)
	}
